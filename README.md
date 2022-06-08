## How to make .aab bundle for uploding on google play store
### 
https://stackoverflow.com/questions/26449512/how-to-create-a-signed-apk-file-using-cordova-command-line-interface

### Key Generation:
keytool -genkey -v -keystore <keystoreName>.keystore -alias <Keystore AliasName> -keyalg <Key algorithm> -keysize <Key size> -validity <Key Validity in Days>

ex
keytool -genkey -v -keystore MytestApp.keystore -alias MytestApp -keyalg RSA -keysize 2048 -validity 10000

keytool, jarsigner in jdk
C:\Program Files\Java\jdk<-version.number.some>\bin
to Path

jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <keystorename> <Unsigned APK file> <Keystore Alias name>

ex
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore MytestApp.keystore app-release.aab Mytestapp

jarsigner in sdk build tools


zipalign in sdk
C:\Users\<username>\AppData\Local\Android\Sdk\build-tools\<version.tools>
to Path
