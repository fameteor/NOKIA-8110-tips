# Driver problem on Windows

Go to "gestionnaire de périphériques" and reinstall a local driver : SAMSUNG Android Composite ADB Interface.

Then launch `/adb/debug`

# Update root certificate

See : https://github.com/openGiraffes/b2g-certificates : launch the batch after setting the contact between Windows and the nokia in DEBUG and ROOT mode.


# Debug mode
- `*#*#33284#*#*`

# Connect to firefox
- `adb forward tcp:6000 localfilesystem:/data/local/debugger-socket`

# Upload with GDEPLOY (https://gitlab.com/suborg/gdeploy)
