# React Native Deployment

This tutorial shall help deploying your React Native App binaries to the App Store (iOS) and Play Store (Android).

We are NOT covering 
- how to set up an Apple Developer Account (https://developer.apple.com/) or Google Developer Account (https://play.google.com/apps/publish/)
- how to create an App in App Store Connect, former iTunes Connect (https://appstoreconnect.apple.com/), or in Google Play Console (https://play.google.com/apps/publish/signup/)
- how to add Meta Data and Promo Pictures / Videos to your created App


## Table of Contents

1. [Coming from 3 different Setups](#chapter1)
    1. [Deployment of Apps built with `Create React Native App` Starter Kit](#chapter1a)
    2. [Deployment of Apps built with `Expo`](#chapter1b)
    3. [Deployment of Apps built with `React Native CLI`](#chapter1c)
2. [Links](#chapter2)


## <a id="chapter1"></a>1. Coming from 3 different Setups

This tutorial is the last step in my little React Native tutorial series:

1. React Native Setup: https://github.com/herrkraatz/react-native-setup
2. React Native Styling: https://github.com/herrkraatz/react-native-styling
3. React Native Deployment: https://github.com/herrkraatz/react-native-deployment

It shows you how to build your

- Apple App Store package IPA (iPhone Application Archive) and 
- Google Play Store package APK (Android PacKage)

for upload into the Stores.

Preferences: 

- Your React Native App was developed using one of the three options in https://github.com/herrkraatz/react-native-setup
- Your software / tools / frameworks with that you developed the React Native App are still installed.

Ok, now let's dive into it.

## <a id="chapter1a"></a>i. Deployment of Apps built with `Create React Native App` Starter Kit

### You have 2 options here:

1. The Standard: Use Expo's `exp build` command

    See great documentation on https://docs.expo.io/versions/latest/guides/building-standalone-apps.html
    
    And please jump to [Deployment of Apps built with `Expo`](#chapter1b) here in this tutorial   

2. Advanced: If you need to integrate your `Create React Native App` (CRNA) into an existing native iOS / Android application OR want to create custom native modules beyond the standard React Native Components / APIs,

    - you need to "eject" from `Create React Native App` using `npm run eject`: See https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md#ejecting-from-create-react-native-app
    - you need to use `react-native-cli` along with Xcode and Android tools: 
        - See https://github.com/herrkraatz/react-native-setup#chapter1c
        - See Tab "Building Projects with Native Code" on https://facebook.github.io/react-native/docs/getting-started.html
    - when done, jump to [Deployment of Apps built with `React Native CLI`](#chapter1c) here in this tutorial
    
    One disadvantage of ejecting is that after you've ejected from CRNA, you don't get to use CRNA's tools and it won't take care of upgrades for you in the future.

    Also see https://stackoverflow.com/questions/42967465/created-an-app-with-create-react-native-app-how-to-publish-it-to-the-google-pla

## <a id="chapter1b"></a>ii. Deployment of Apps built with `Expo`

First see great documentation on https://docs.expo.io/versions/latest/guides/building-standalone-apps.html

Here's a quick summary of it:

1. Install `exp`
    
    Open a Terminal window and run:
    
    ```
    > npm install -g exp
    ```
    
2. Configure app.json

    ```
    {
       "expo": {
        "name": "Your App Name",
        "icon": "./path/to/your/app-icon.png",
        "version": "1.0.0",
        "slug": "your-app-slug",
        "sdkVersion": "XX.0.0",
        "ios": {
          "bundleIdentifier": "com.yourcompany.yourappname"
        },
        "android": {
          "package": "com.yourcompany.yourappname"
        }
       }
     }
     ```
     
     See https://docs.expo.io/versions/latest/guides/building-standalone-apps.html#2-configure-appjson for details
     
3. Make the build

    Run for iOS:

    ```
    > exp build:ios
    ```
    
    Run for Android:
    
    ```
    > exp build:android
    ```
    
4. Download the IPA / APK file from Expo Server

    See https://docs.expo.io/versions/latest/guides/building-standalone-apps.html#4-wait-for-it-to-finish-building
    
5. Final test on Device or Simulator / Emulator

    See https://docs.expo.io/versions/latest/guides/building-standalone-apps.html#5-test-it-on-your-device-or
  
6. Prepare the Stores

    - Create the App within App Store Connect and Google Play Console
    - iOS: Make sure to use the same bundle ID as in bundleIdentifier of app.json file (above).
    
6. Submit it to the Stores

    First please see https://docs.expo.io/versions/latest/guides/app-stores.html
    
    Also you need to add this to your App:
    
    - Adding Launcher App Icons: https://docs.expo.io/versions/v28.0.0/guides/app-icons
    
    Probably these, too:
    
    - Adding Splash Screens: https://docs.expo.io/versions/latest/guides/splash-screens
    - Configuring Status Bar: https://docs.expo.io/versions/v28.0.0/guides/configuring-statusbar


## <a id="chapter1c"></a>iii. Deployment of Apps built with `React Native CLI`

1. iOS

    - Add Launcher App Icons: Go to Xcode >> Project Folder >> Images.xcassets >> AppIcon and add all necessary Launcher App Icons you generated. I can recommend "Icon Slate" App to generate all sizes of Launcher App Icons.

    - Add Splash Screens: 
        - Check out https://github.com/crazycodeboy/react-native-splash-screen OR
        - Go to Xcode >> Project Folder >> LaunchScreen.xib and manually create your own Splash Screen
    
    - Now create an App in the App Store Connect, in order to upload the IPA into it. Make sure to use the same bundle ID as in your Xcode project.

    - Then check out https://facebook.github.io/react-native/docs/running-on-device.html#building-your-app-for-production
    
    - Once all is configured there, you can deploy your App from Xcode (from your machine):
    
        - First create an Archive by running "Product" => "Archive" in Xcode.
        - From the popped up Archive Explorer you can then upload the App to App Store Connect (former iTunes Connect).
        - Read more under https://help.apple.com/xcode/mac/current/#/dev442d7f2ca
        
2. Android

    - Add Launcher App Icons: Go to Android Studio >> android >> app >> src >> main >> res Folder and add all necessary Launcher App Icons you generated. I can recommend "Icon Slate" App to generate all sizes of Launcher App Icons.

    - Add Splash Screens: 
        - Check out https://github.com/crazycodeboy/react-native-splash-screen OR
        - Go to Android Studio >> android >> app >> src >> main >> java >> com >> Project Folder >> MainActivity.java and insert Splash Screen sections there
        
    - Now create an App in the Google Play Console, in order to upload the APK into it.

    - Then build and sign the App. Signing is done to ensure your uploaded APK is clearly indentified: 
    
        See instructions:
        - https://facebook.github.io/react-native/docs/signed-apk-android
        - https://facebook.github.io/react-native/docs/running-on-device.html#building-your-app-for-production-1

    - Manually upload the APK into the created App in Google Play Console


## <a id="chapter2"></a>2. Links

### Have a look !


Apple:
- Developer Account: https://developer.apple.com/
- App Store Connect: https://appstoreconnect.apple.com/
- Upload an App: https://help.apple.com/xcode/mac/current/#/dev442d7f2ca

Google:
- Developer Account/Play Console: https://play.google.com/apps/publish/

Deployment:
- Maximilian Schwarzmüller, Udemy Course: "React Native - The Practical Guide": https://www.udemy.com/react-native-the-practical-guide/
- React Native: https://facebook.github.io/react-native/docs/running-on-device.html
- Expo: https://docs.expo.io/versions/latest/guides/building-standalone-apps.html
- Expo: https://docs.expo.io/versions/latest/guides/app-stores.html

Debugging:
- How To: https://facebook.github.io/react-native/docs/debugging.html
- How To: https://facebook.github.io/react-native/docs/running-on-device.html
- Standalone React Developer Tools for a proper React "DOM tree" and more: https://github.com/facebook/react-devtools/tree/master/packages/react-devtools
- Standalone React Native Debugger for integrated React "DOM" manipulation and Redux: https://github.com/jhen0409/react-native-debugger

Create React Native App (CRNA) Starter Kit: 
- See Tab "Quickstart" on https://facebook.github.io/react-native/docs/getting-started.html
- CRNA Repo: https://github.com/react-community/create-react-native-app
- https://facebook.github.io/react-native/docs/running-on-device.html
- React Native Home: https://facebook.github.io/react-native
- React Native Repo: https://github.com/facebook/react-native

Expo:
- Home: https://expo.io/
- List of components: https://docs.expo.io/versions/latest/sdk/index.html (left column)

React Native CLI:
- See Tab "Building Projects with Native Code" on https://facebook.github.io/react-native/docs/getting-started.html
- https://facebook.github.io/react-native/docs/running-on-device.html
- React Native Home: https://facebook.github.io/react-native
- React Native Repo: https://github.com/facebook/react-native


### Credits to the authors of above links ! Thank you very much !

### And credits to the reader: Thanks for your visit !