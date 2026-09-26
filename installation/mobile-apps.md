---
description: Native IAB TCF consent for iOS and Android with the Okito mobile SDK.
---

# iOS and Android apps

Okito's mobile SDKs show a native consent banner and preference centre, create the IAB TCF string and store it where ad SDKs expect it. They are pure native (SwiftUI on iOS, Jetpack Compose on Android); no WebView is needed.

## Set up the app in Okito

1. In the dashboard, add a new property and choose **Mobile app**. Enter the app name, platform (iOS or Android) and the bundle ID / package name.
2. Configure the consent screen in Banner Builder (the **Mobile SDK** tab).
3. Open **Install banner**. It shows the initialisation code for your app, with your website ID and API address filled in.

## iOS (Swift Package)

Requirements: iOS 15+ / tvOS 15+, Swift 5.9+.

Add the Okito `mobile-sdk` Swift package in Xcode (**File → Add Package Dependencies**; contact [info@okito.com](mailto:info@okito.com) for the repository address) and add the `OkitoCMP` product to your target:

```swift
.product(name: "OkitoCMP", package: "mobile-sdk")
```

Then initialise it at app start with the code from Install banner:

```swift
import OkitoCMP

OkitoCMP.shared.initialize(.init(
    baseURL: URL(string: "COPY_FROM_INSTALL_BANNER")!,
    websiteId: "COPY_FROM_INSTALL_BANNER",
    visitorId: UUID().uuidString,
    publisherCountryCode: "TR",
    consentLanguage: "EN",
    cmpSdkId: 508,
    cmpSdkVersion: 1
))
```

## Android (Maven Central)

Requirements: Android API 21+, Kotlin 1.9+, Jetpack Compose.

```kotlin
dependencies {
    implementation("io.okito:cmp:1.0.0")
}
```

Initialise it in your `Application` class with the code from Install banner:

```kotlin
OkitoCMP.initialize(
    context = this,
    options = OkitoCMP.InitOptions(
        baseUrl = "COPY_FROM_INSTALL_BANNER",
        websiteId = "COPY_FROM_INSTALL_BANNER",
        visitorId = java.util.UUID.randomUUID().toString(),
        publisherCountryCode = "TR",
        consentLanguage = "EN",
        cmpSdkId = 508,
        cmpSdkVersion = 1,
    ),
)
```

## API

Both SDKs mirror the web `__tcfapi`:

| Call | What it does |
| --- | --- |
| `acceptAll()` / `rejectAll()` | Save a choice without the UI. |
| `save(purposes, vendors, specialFeatures, …)` | Save a granular choice. |
| `getTCData()` | The current TC data, or none if the user hasn't chosen yet. |
| `addEventListener { … }` / `removeEventListener(id)` | Be notified when consent changes. |
| `reset()` | Clear the stored consent. |
| `cmpStatus`, `eventStatus` | Loading state and the last event, as in `__tcfapi`. |

## Where consent is stored

The SDKs write the standard `IABTCF_*` keys to `UserDefaults.standard` (iOS) and the default `SharedPreferences` (Android). Ad SDKs such as Google Mobile Ads, AppLovin MAX, ironSource, Unity Ads, Pangle, Mintegral and Vungle read these keys automatically.

## Google Consent Mode for Firebase

If your app uses Google Analytics for Firebase, the SDK sets Firebase consent (`Analytics.setConsent`) at start-up and after every choice. Pass `firebaseConsentMode: false` in the options to turn it off.

## Test it

The SDK repository includes demo apps for both platforms with a verification panel that shows every stored `IABTCF_*` key and checks the setup.
