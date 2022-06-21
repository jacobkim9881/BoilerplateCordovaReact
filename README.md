## How to build android app for uploading on google play store

### Add android from cordova

```

cordova platform add android

```

### Build android app 

```

cordova build android

```

### Get release app 
Go to `path\to\your\Project\platforms\android\` and run this,

```

./gradlew bundle

```

So at `path\to\your\Project\platforms\android\app\build\outputs\bundle\release\` there will be `.aab` file for uploading. Sign key store and zipalign like below.

## How to make .aab bundle for uploding on google play store
To upload .apk or .aab file on google play store console, the file should have keystore with. [Reference here](https://stackoverflow.com/questions/26449512/how-to-create-a-signed-apk-file-using-cordova-command-line-interface).

### Remove unneeded plugin
Remove cordova console at `C:\path\to\your\Projects\` by typing 

```

cordova plugin rm org.apache.cordova.console --save

```

but in my case the plugin wasn't added at first. 

### Edit debugable to false at AndroidManifest.xml
AndroidManifest.xml will be placed at `path\to\your\Project\platforms\android\CordovalLib\AndroidManifest.xml` since you have added android version for cordova. Open the xml file and edit this tag from

```

<application android:debuggable="true" android:hardwareAccelerated="true" android:icon="@drawable/icon" android:label="@string/app_name">


```

to

```

<application android:debuggable="false" android:hardwareAccelerated="true" android:icon="@drawable/icon" android:label="@string/app_name">


```

but in my case this property of the tag was set false at first.

### Key Generation
If you don't have keystore then create one for adding it to .apk or .aab at `path\to\your\Project\platforms\android\app\build\outputs\bundle\release\`. If you don't have command then add one by following ##Environment below. Type like on command,

```

keytool -genkey -v -keystore <keystoreName>.keystore -alias <Keystore AliasName> -keyalg <Key algorithm> -keysize <Key size> -validity <Key Validity in Days>

```

Example like,

```

keytool -genkey -v -keystore MytestApp.keystore -alias MytestApp -keyalg RSA -keysize 2048 -validity 10000

```


### Add keystore to .apk or .aab file
To add keystore to .apk or .aab file, jarsigner commanded needed at `path\to\your\Project\platforms\android\app\build\outputs\bundle\release\`. Type like,

```

jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <keystorename> <Unsigned APK file> <Keystore Alias name>

```

For example,

```

jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore MytestApp.keystore app-release.aab Mytestapp

```


### zipalign the .apk or .aab file
Finally zipalign the file at `path\to\your\Project\platforms\android\app\build\outputs\bundle\release\`. So the apk file is ready for uploading.

```

zipalign -v 4 Example-release-unsigned.apk Example.apk

```

## Upload test version on google play console
Proceed login at `https://play.google.com/console/about/` first.

### Register tester
Go to Internal test and start to register tester at tester tab. After register tester with each email you can use test version.

### Make test version at tester tab
Make new test version by clicking make new version at tester tab.

### Upload signed .aab file to test version
.aab file should be signed with key store and zipalign.

## Download test version 
At tester tab of Internal test, there will be like `join at web`. Click `copy link` and proceed the link at your smartphone which is registered as a tester.

## Environment
### Add specific command on windows
[Reference here](https://superuser.com/questions/689333/how-to-add-installed-program-to-command-prompt-in-windows).
- right click my computer
- click Properties
- click Advanced System Settings
- click Environment Variables
- In the bottom pane find Path, select it and click Edit
- click make new button, then click find
- set the path you want to added command for example, `C:\Users\name\AppData\Local\Android\Sdk\build-tools\30.0.3`

### Add keytool, jarsigner command on your path 
keytool and jarsigner commands are in jdk. Add the path on Path at Environment Variables on windows.
`C:\Program Files\Java\jdk<-version.number.some>\bin`

### zipalign
zipalign is in in sdk. Add the path on Path at Environment Variables on windows.

`C:\Users\<username>\AppData\Local\Android\Sdk\build-tools\<version.tools>`
