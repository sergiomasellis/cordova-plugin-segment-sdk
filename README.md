# Segment Analytics Cordova Plugin

Cordova plugin for Segment Analytics. Supports Segment's iOS and Android SDKs.

## Usage
Implements the same interface as the iOS and Android native Segment SDK.


## Installation

`ionic cordova plugin add https://github.com/pidal/cordova-plugin-segment-sdk`

## Configuration

In the projects config.xml add the following preferences with the Segment source keys

## Usage

1. Inject the service dependency on the component where it's going to be needed: 

` constructor(private analyticsService: AnalyticsService) {} `

2. Use the methods provided: .track, .alias(), .identify(), .alias(), etc...
For more information check official Segment iOS and Android SDK.

`this.analyticsService.track('Button pressed Service');`

It might be useful to send some events or setup configurations on the initializeApp() ionic method:

```typescript
initializeApp() {
    this.platform.ready().then(() => {
      this.statusBar.styleDefault();
      this.splashScreen.hide();

      this.initializeAnalytics();

    });
  }

  initializeAnalytics(): any {
      this.analyticsService.track('Application Opened', {}, {});
  }
```


### iOS

Inside `<platform name="ios">`element: 

`<preference name="ios_segment_write_key" value="{Segment iOS write key}" />`

### Android

Inside `<platform name="android">` element:

`<preference name="android_segment_write_key" value="{Segment Android write key}" />`

## Dependencies

This plugins requires the [IDFA plugin][] to be able to get the Advertising ID from the device and send it within the request to Segment.

This is needed for some integrations to work properly, such as a Facebook App Events


## iOS Integrations Setup
This plugin uses cordova-plugin-cocoapods-support to automatically bundle in the Segment iOS SDK through CocaoPods.

The only caveat is that you will need to run the project from AppName.xcworkspace instead of AppName.xcodeproj (this is a limitation introduced by CocoaPods itself).

Also for this reason, if you are using Ionic and its command line tools, `ionic build` and `ionic run` will cause the archive build to fail. You will need to manually run the project in Xcode from AppName.xcworkspace.

You might also want to consult official Segment documentation [iOS Quickstart][].

## Android Integrations Setup
Use Gradle:
By default, the plugin builds with the `analytics-core` SDK for Android.
To add more your custom integrations, create a `build-extras.gradle` file in your Android platform root directory and add your segment integration dependencies. See the [Android Custom Build Docs][] for examples.

[Analytics.js]: https://segment.io/docs/libraries/analytics.js
[iOS Quickstart]: https://segment.com/docs/libraries/ios/quickstart/
[Android Custom Build Docs]: https://segment.com/docs/libraries/android/#custom-builds
[IDFA plugin]: https://www.npmjs.com/package/cordova-plugin-idfa
