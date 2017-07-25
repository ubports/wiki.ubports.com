Developers of a web application will probably do most of their coding and debugging in the usual desktop browser environment.  Because UBports' browser has excellent compliance with modern web standards, such code will most often operate on the UBports browser without further changes.

For those (hopefully) rare cases where further debugging is needed, there are two ways to gain further information on the failure.
## Simple CLI
If you are comfortable in a CLI environment, you can launch the _Terminal_ application, and then view the file:
    .cache/upstart/application-legacy-webbrowser-app-.log
Most Javascript errors will leave an entry in this file.
## Browser Debugger
The native UBports web browser, known as _webbrowser-app_, is based on Google's _Blink_ technology, which also powers their _Chrome_/_Chromium_ browsers.  By starting your phone's browser in a special mode, you have access to the regular Chrome-style debugger.
#### Stop your browser
Swipe from the right to get the process list, then drag downward on the pane for the browser to tell the process to exit.
#### Start the browser in _inspector_ mode
Launch the Terminal app.  Then launch the UBports web browser in _inspector_ mode:
    ubuntu-app-launch webbrowser-app --inspector
If you don't already know your phone's local IP address, do:
    ifconfig
and look for the IP address under the wlan0 entry.  It'll be the "inet addr" one unless you're on the more modern IPv6 style of network, in which case it's the "inet6 addr".  If you have to guess, start with the "inet addr" one.
#### Fire up a desktop Chrome/Chromium browser
Open a new tab, type control-L to select the current address, then type in:
    http://YOUR-IP-ADDR:9221
If all goes well, you'll get a list of the current tabs on your UBports device.  Choose one, and you will be in a familiar Chrome-style debug environment for that tab on your phone.