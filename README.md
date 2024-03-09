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

# Network filtering : iptables
- `iptables-save` doesn't work
- `ip6tables -L -v   ` also works

```
iptables -L -v
Chain INPUT (policy ACCEPT 4643 packets, 3813K bytes)
 pkts bytes target     prot opt in     out     source               destination         
 4643 3813K bw_INPUT   all  --  any    any     anywhere             anywhere            
 4643 3813K fw_INPUT   all  --  any    any     anywhere             anywhere            

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 oem_fwd    all  --  any    any     anywhere             anywhere            
    0     0 fw_FORWARD  all  --  any    any     anywhere             anywhere            
    0     0 bw_FORWARD  all  --  any    any     anywhere             anywhere            
    0     0 natctrl_FORWARD  all  --  any    any     anywhere             anywhere            

Chain OUTPUT (policy ACCEPT 3297 packets, 333K bytes)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 DROP       udp  --  any    rmnet_data7  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data6  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data5  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data4  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data3  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data2  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data1  anywhere             anywhere             udp dpt:1900
    0     0 DROP       udp  --  any    rmnet_data0  anywhere             anywhere             udp dpt:1900
 3297  333K oem_out    all  --  any    any     anywhere             anywhere            
 3297  333K fw_OUTPUT  all  --  any    any     anywhere             anywhere            
 3297  333K st_OUTPUT  all  --  any    any     anywhere             anywhere            
 3297  333K bw_OUTPUT  all  --  any    any     anywhere             anywhere            

Chain bw_FORWARD (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain bw_INPUT (1 references)
 pkts bytes target     prot opt in     out     source               destination         
 4447 3800K            all  --  any    any     anywhere             anywhere             owner socket exists

Chain bw_OUTPUT (1 references)
 pkts bytes target     prot opt in     out     source               destination         
 3235  330K            all  --  any    any     anywhere             anywhere             owner socket exists

Chain bw_costly_shared (0 references)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 bw_penalty_box  all  --  any    any     anywhere             anywhere            

Chain bw_happy_box (0 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain bw_penalty_box (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain fw_FORWARD (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain fw_INPUT (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain fw_OUTPUT (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain fw_dozable (0 references)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 RETURN     all  --  any    any     anywhere             anywhere             owner UID match 0-9999
    0     0 DROP       all  --  any    any     anywhere             anywhere            

Chain fw_standby (0 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain natctrl_FORWARD (1 references)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 DROP       all  --  any    any     anywhere             anywhere            

Chain natctrl_tether_counters (0 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain oem_fwd (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain oem_out (1 references)
 pkts bytes target     prot opt in     out     source               destination         

Chain st_OUTPUT (1 references)
 pkts bytes target     prot opt in     out     source               destination    
```


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
