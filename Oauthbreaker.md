# Background and setup
- Install genymotion to simulate android environment.
- In gentoo, `emerge --ask genymotion-bin`
- Launch with `QT_QPA_PLATFORM=xcb genymotion` if using swaywm
- AndroidManifest.xml is an important file in each android application
- In android development, `intents` is the message from system or other apps.
- In AndroidManifest.xml specify intents filter, which prevent the outside call the internal component of the app.


# The oauth.apk
- It is the zip format file
- The flow of the application is: Open app -> press authenticate button -> app open website -> click link on website -> the app successfull authenication
- In burpsuite, the app send a request to ctf server, the server reply with a token.

# Exploit 
- Will be back later
