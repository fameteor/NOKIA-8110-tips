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

# Development :
- Gerda installation : https://mis.pm/banana-hack#gerdaos
- webapps are located in : `/data/local/webapps`
- sdcard is mounted on : `/storage/sdcard`
## Documentation :
- KAIOS 2.5 permissions detail : https://developer.kaiostech.com/docs/getting-started/main-concepts/permissions/
- Manifest items full guide : https://kaios.dev/2023/03/complete-manifest.webapp-guide/
- Manifest permissions guide : https://kaios.dev/2023/03/complete-kaios-permission-guide/
- B2G security constraints : https://wiki.mozilla.org/Apps/Security
