# Driver problem on Windows

Go to "gestionnaire de périphériques" and reinstall a local driver : SAMSUNG Android Composite ADB Interface.

Then launch `/adb/debug`

# Update root certificate

See : https://github.com/openGiraffes/b2g-certificates : launch the batch after setting the contact between Windows and the nokia in DEBUG and ROOT mode.


# Debug mode
- `*#*#33284#*#*`

# Connect to firefox
- `adb forward tcp:6000 localfilesystem:/data/local/debugger-socket`

# Access to Linux shell as `root` : 
- lauch the ROOT application
- connect USB to PC
- in a terminal window : `adb shell`

# Use network analyser `tcpdump`

- use `tcpdump -D` to get the interface list
- capture until `CTRL C` on `any` interface : `tcpdump -i any`
- capture to a file : `tcpdump -i any -s 65535 -w /storage/sdcard/dumps/myFile.pcap`
- analyse with `Wireshark`

# Upload with GDEPLOY (https://gitlab.com/suborg/gdeploy)

# Development :
- Gerda installation : https://mis.pm/banana-hack#gerdaos
- webapps are located in : `/data/local/webapps`
- sdcard is mounted on : `/storage/sdcard`
## Documentation :
- KAIOS 2.5 permissions detail : https://developer.kaiostech.com/docs/getting-started/main-concepts/permissions/
- KAIOS 2.5 API : https://developer.kaiostech.com/docs/api/web-apis
- Manifest items full guide : https://kaios.dev/2023/03/complete-manifest.webapp-guide/
- Manifest permissions guide : https://kaios.dev/2023/03/complete-kaios-permission-guide/
- B2G security constraints : https://wiki.mozilla.org/Apps/Security
- Can I use for KAIOS browser : https://caniuse.com
- TIPS development KAIos : https://kaios.dev/

# Developper Tips : 
- Check if Internet available : boolean value : `navigator.onLine` . Events are associated : `window.addEventListener('online',  callbackFunction);` and `window.addEventListener('offline', callbackFunction);`

## Screen layout

There can be 4 orientations :
- `portrait-primary` 	(normal position)
- `portrait-secondary` 	(phone upside down)
- `landscape-primary` 	(keyboard on the right)
- `landscape-secondary` (Keyboard on the left)

To change the orientation, you can :
- use the Manifest : `"orientation": "landscape"`. See Manifest documentation for more informations.
- or with Javascript : `screen.orientation.lock('landscape-primary');`

To get the value of the orientation : `screen.orientation.type`

A KaiOs app has the following layout (from top to bottom) :
- KaiOs status (notifications, battery, time ...) : height is 25 px.
- the appTitle : height 20 px.
- the application zone : the remaining height.
- the softkeys zone : height : 30 px.

To hide the status bar, you can use the Manifest : `"fullscreen": "true"`
