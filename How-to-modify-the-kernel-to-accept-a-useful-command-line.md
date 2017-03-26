Things can get really nasty with mobile devices. Say, you want to append a few things to the kernel command line for booting with special instructions.

Like you basically need at least the following parameter in your kernel command line:

    console=tty0

(See [here](https://wiki.ubuntu.com/Touch/ContainerArchitecture) why, first few paragraphs)

But here comes the problem: The bootloader itself wants to offload a ton of strange cmdline arguments and overwrites your cmdline string just before the kernel starts. So how to get it there then?

- Go to your kernel config file
- Set CONFIG_CMDLINE="console=tty0"
- Set CONFIG_CMDLINE_EXTEND=y

Unfortunately this works only in theory. The EXTEND feature appends actually the bootloader cmdline AFTER ours. Some bootloaders have console=none or console=ram hardocded into their string. This will effectively overwrite our command again. What to do?

- Apply the following patch to your kernel:

```
--- arch/arm/kernel/setup.c.orig	2013-08-02 12:30:00.467880848 +0200
+++ arch/arm/kernel/setup.c	2013-08-02 12:12:01.659851483 +0200
@@ -669,9 +669,11 @@
 static int __init parse_tag_cmdline(const struct tag *tag)
 {
 #if defined(CONFIG_CMDLINE_EXTEND)
+	char tmp[COMMAND_LINE_SIZE];
+	strlcpy(tmp, default_command_line, COMMAND_LINE_SIZE);
+ 	strlcpy(default_command_line, tag->u.cmdline.cmdline, COMMAND_LINE_SIZE);
 	strlcat(default_command_line, " ", COMMAND_LINE_SIZE);
-	strlcat(default_command_line, tag->u.cmdline.cmdline,
-		COMMAND_LINE_SIZE);
+	strlcat(default_command_line, tmp, COMMAND_LINE_SIZE);
 #elif defined(CONFIG_CMDLINE_FORCE)
 	pr_warning("Ignoring tag cmdline (using the default kernel command line)\n");
 #else
 ```
 
This will modify the way the cmdline is loaded in such a way so that our cmdline comes AFTER the bootloader cmdline. Very neat!
 
Last issue: The length. Some bootloaders totally overload the cmdline string, so that any character we append might get eaten up. It´s true! What to do?

Open your kernels /arch/arm/include/setup.h file and set:
     
     #define COMMAND_LINE_SIZE 2048
 
This should be enough even for the most bloated bootloaders on this planet!