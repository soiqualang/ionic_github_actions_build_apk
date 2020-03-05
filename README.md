# ionic_github_actions_build_apk
ionic_github_actions_build_apk

`ionic cordova prepare android`

https://github.com/features/actions

https://help.github.com/en/actions/reference/virtual-environments-for-github-hosted-runners

https://stackoverflow.com/questions/18328730/how-to-create-a-release-signed-apk-file-using-gradle

***

Easier way than previous answers:

Put this into `~/.gradle/gradle.properties`

```bash
RELEASE_STORE_FILE={path to your keystore}
RELEASE_STORE_PASSWORD=*****
RELEASE_KEY_ALIAS=*****
RELEASE_KEY_PASSWORD=*****
```

Modify your `build.gradle` like this:

```bash
...    
signingConfigs {

   release {
       storeFile file(RELEASE_STORE_FILE)
       storePassword RELEASE_STORE_PASSWORD
       keyAlias RELEASE_KEY_ALIAS
       keyPassword RELEASE_KEY_PASSWORD
   }
}

buildTypes {
        release {
            signingConfig signingConfigs.release
        }
}
....
```

Then you can run `gradle assembleRelease`