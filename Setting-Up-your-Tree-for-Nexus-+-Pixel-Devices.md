Please note that Libhybris is currently not working for any Marshmallow device.

This article was originally going to contain instructions for getting sources from other manufacturers' open source repositories as well, but I quickly decided against that after looking at Motorola's GitHub. It's a mess.

The Android source tree is all of the code and prebuilt binaries that go into your device's Android build. Your tree is going to be the most important part of your building journey, so it's important to set it up right!

You can go and read the beginning of [[Setting-up-Your-Tree-for-CM12.1-Devices]], up to the information about getting your branch. That's where this document will take off.

### Who is this document for?

If you have a Nexus device that has an official Android 6.0 Marshmallow build, this is for you. There are also some Sony devices that this information will help with, but that's probably a topic for another document since their sources are on Github rather than Googlesource.

Basically, if your device is on [this page](https://source.android.com/source/building-kernels.html) and has Android 6.0, read on!

### Getting the Initial Sources

Every journey begins with the first step, so let's take ours. You'll need to get Repo ready to grab the 6.0 phablet sources.

`repo init -u https://code-review.phablet.ubuntu.com/p/aosp/platform/manifest.git -b phablet-6.0.0_r1`

## Adding your Device-Specific Stuff

Okay, so now you have the default manifest for Ubuntu Touch. This will enable you to download the basic Android sources used to build Ubuntu Touch, but you'll need to find device-specific files. These enable the build tree to make Android for your device.

### The Local Manifest


Change into your `~/phablet` directory and create the directory `.repo/local_manifests`. Then, edit the file `.repo/local_manifests/[manufacturer]_[device].xml`. 

Paste the following information into it, then save:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

</manifest>
```

This is the base information required for the file to be a local manifest.


### Adding your Device Repository

The device repository allows the Android build system to make the whole system image for your device. It's a pretty big deal.

Luckily, it's really easy to find AOSP device trees. Just head on over to [Google's Git](https://android.googlesource.com/?format=HTML) and find your device in the list by codename. The repository name will look like "device/[manufacturer]/[codename]". Click on the repository to open it. You'll come to the overview page for the repository. There's not too much interesting here, except for the `More...` links under `Branches`. Click it now.

Find the latest branch of the repository. For many Marshmallow devices, this will be `marshmallow-dr1.6-release`. If not, check out the branches and find the one with the newest commits.
"Now," I hear you say, "What does dr1.6 stand for?" 
Well... I have no idea. And I can't find any documentation for it. So you're going to have to trust me.

Knowing the latest branch of your device, you can create a line in the local manifest for it. Let's do that now. Replace all of the bracketed items with your information.

```xml
<project path="device/[manufacturer]/[device]" name="[repository name]" remote="aosp" revision="[name of revision you found]" />
```

The project tag tells repo to make another git repository as we specify. The path tells it where in our tree the project will go. It always follows the convention listed above, manufacturer then device codename.

The repository name in AOSP is always the path after `android.googlesource.com/`. For example, for the Nexus 5X, the Googlesource URL is `https://android.googlesource.com/device/lge/bullhead/`, so the repository name is `device/lge/bullhead`. Simple, right? Right.


### Syncing your repository

Simple. Run `repo sync -j4` to sync all of the good stuff from the Interwebs to your computer. You may consider putting in a larger job number (`-jX`) if you have a hefty internet connection.

### Adding your Vendor stuff

Vendor stuff may be a little more involved, or it may not be. Check [this page](https://developers.google.com/android/nexus/drivers) for your desired device. If it's there, your job is easy: Download all the packages, extract them, run the script, accept the license agreement, and it gives you the files all packaged up in `./vendor`. Once you have all of the files extracted, copy them into your tree so that you have `~/phablet/vendor`. You're done. Congrats.

For other phones, *cough* Nexus 5X and 6P, your job is a little more difficult. You can use the scripts from [this repository](https://github.com/anestisb/android-prepare-vendor) to retrieve the blobs from a factory image. So, clone the repo, read the README, and have some fun. I'll be here when you get back.

All good? Alright. Copy the `vendor` folder from the output of the script (it'll be a few levels deep) into `~/phablet` so that you have `~/phablet/vendor`, just like the people with *good* phones do. Since you need to run some scripts with sudo, you might need to run `chown` on the files first to make them yours.

### Conclusion

If you followed everything here and you have your `device/[manufacturer]/[device]` and `vendor/[manufacturer]/[device]` folders, you're probably good to go! You should consider using `tar` to make a backup of your tree that you can restore in case anything bad happens.

However, that doesn't mean that you're ready to build yet. You'll need to get and build a kernel for your device, which will be discussed in another article.