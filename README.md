# rn-codepush
POC for creating a React Native app that is updated via CodePush

## Steps

1. Go to Microsoft's [AppCenter](https://www.appcenter.ms/apps) and create an account.
2. Install AppCenter CLI, add one app for Android and one for iOS, create and copy their deployment keys:

```bash
$ npm install -g appcenter-cli
$ appcenter login
# Create apps at AppCenter
$ appcenter apps create -d rn-codepush-Android -o Android -p React-Native
$ appcenter apps create -d rn-codepush-iOS -o iOS -p React-Native
# Create deployment keys
$ appcenter codepush deployment add -a <appcenter-username>/rn-codepush-Android Staging
$ appcenter codepush deployment add -a <appcenter-username>/rn-codepush-Android Production
$ appcenter codepush deployment add -a <appcenter-username>/rn-codepush-iOS Staging
$ appcenter codepush deployment add -a <appcenter-username>/rn-codepush-iOS Production
# Copy the production deployment key for Android
$ appcenter codepush deployment list -a <appcenter-username>/rn-codepush-Android
# Copy the production deployment key for iOS
$ appcenter codepush deployment list -a <appcenter-username>/rn-codepush-iOS
```

3. Initialize RN app, add CodePush dependency and link it:

```bash
$ react-native init rn_codepush
$ cd rn_codepush
$ yarn add react-native-code-push
$ react-native link react-native-code-push
```

4. Follow this [instructions](https://facebook.github.io/react-native/docs/running-on-device) to create production builds for both platforms.
5. Install and open the production builds on a device or emulator.
6. Make changes to the JS files on the project.
7. [Release](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/cli#releasing-updates-react-native) a new version through CodePush:

```bash
$ appcenter codepush release-react -a <appcenter-username>/rn-codepush-Android -d Production -t "*" -m
$ appcenter codepush release-react -a <appcenter-username>/rn-codepush-iOS -d Production -t "*" -m
```

8. Close and reopen the app. The old version should appear at first, the app should blink and the new version should automatically load.
