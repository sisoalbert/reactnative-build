# reactnative-build

React-native-debug
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res

cd android

./gradlew assembleDebug

yourProject/android/app/build/outputs/apk/debug/app-debug.apk


React-native-signed-APK

/Generating a signing key #
//generate a private signing key using keytool.

keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

//Setting up gradle variables #
Place the my-release-key.keystore file under the android/app directory in your project folder.
Edit the file ~/.gradle/gradle.properties and add the following (replace ***** with the correct keystore password, alias and key password),

MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****

Adding signing config to your app's gradle config #

...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...

Generating the release APK 
$ cd android && ./gradlew assembleRelease

version build.gradle

