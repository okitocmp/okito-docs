---
description: Native IAB TCF consent for iOS and Android with the Okito mobile SDK.
---

# iOS and Android apps

Okito's mobile SDKs show a native consent banner and preference centre, create the IAB TCF string and store it where ad SDKs expect it. They are pure native (SwiftUI on iOS, Jetpack Compose on Android); no WebView is needed.

## Set up the app in Okito

1. In the dashboard, add a new property and choose **Mobile app**. Enter the app name, platform (iOS or Android) and the bundle ID / package name.
2. Configure the consent screen in Banner Builder (the **Mobile SDK** tab). The privacy policy, cookie policy and Aydınlatma Metni links from **Content → Links** appear under the banner text, as on the web ([details](../banner/content-and-languages.md#privacy-policy-and-kvkk-disclosure-notice-links)).
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
    consentLanguage: "EN",
    cmpSdkId: 508,
    cmpSdkVersion: 2
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
        consentLanguage = "EN",
        cmpSdkId = 508,
        cmpSdkVersion = 2,
    ),
)
```

The publisher country in the TC string (`PublisherCC`) comes from your site's settings in the Okito dashboard; the apps don't set it.

## API

Both SDKs mirror the web `__tcfapi`:

| Call                                                 | What it does                                                |
| ---------------------------------------------------- | ----------------------------------------------------------- |
| `acceptAll()` / `rejectAll()`                        | Save a choice without the UI.                               |
| `save(purposes, vendors, specialFeatures, …)`        | Save a granular choice.                                     |
| `getTCData()`                                        | The current TC data, or none if the user hasn't chosen yet. |
| `addEventListener { … }` / `removeEventListener(id)` | Be notified when consent changes.                           |
| `reset()`                                            | Clear the stored consent.                                   |
| `cmpStatus`, `eventStatus`                           | Loading state and the last event, as in `__tcfapi`.         |

## Where consent is stored

The SDKs write the standard `IABTCF_*` keys to `UserDefaults.standard` (iOS) and the default `SharedPreferences` (Android), and `IABTCF_AddtlConsent` (Google's AC string) when Additional Consent is on. Ad SDKs such as Google Mobile Ads, AppLovin MAX, ironSource, Unity Ads, Pangle, Mintegral and Vungle read these keys automatically.

## US state privacy laws

With the [US State Laws template](../banner/consent-templates.md), the app shows the notice and the **Do Not Sell or Share** choice, as on the web. The SDKs store the choice in `IABUSPrivacy_String` and in the IAB Global Privacy Platform keys (`IABGPP_HDR_GppString`, `IABGPP_GppSID` and the other `IABGPP_*` keys), which ad SDKs such as Google Mobile Ads and Prebid read. The GPP string is the same one the web `__gpp` gives for that choice.

The [sensitive data and minors settings](../compliance/us-state-laws.md#sensitive-data-and-sites-for-minors) apply in the app too: when your site says it processes sensitive data, the preference screen asks for consent to its use; on a site directed to minors, US users start opted out, and the Firebase ad consent types (`ad_storage`, `ad_user_data`, `ad_personalization`) start denied until they opt in.

### Web content in the app

Ads or pages in an in-app WebView read the choice through the JavaScript APIs, not the stored keys. Inject them into the WebView after the SDK has read consent, and again after the user changes it:

* `OkitoCMP.shared.gppApiJavaScript()` (iOS) / `OkitoCMP.gppApiJavaScript()` (Android): `window.__gpp`, the IAB GPP API, with the same answers as on the web (`ping`, `addEventListener`, `hasSection`, `getSection`, `getField`). Injected again, it tells the page's listeners about the change.
* `uspApiJavaScript()`: `window.__uspapi`, the US Privacy string.

On iOS, run the script with `webView.evaluateJavaScript(_:)`; on Android, with `webView.evaluateJavascript(script, null)`. A new page in the WebView needs it again.

## Google Consent Mode for Firebase

If your app uses Google Analytics for Firebase, the SDK sets Firebase consent (`Analytics.setConsent`) at start-up and after every choice. Pass `firebaseConsentMode: false` in the options to turn it off.

With IAB TCF, the consent types follow the same purposes as on the web (see [IAB TCF and Google](../google/tcf-and-google.md#tcf-purposes-and-consent-mode)), and in the app all of them also need consent for Google (vendor 755). A purpose you do not allow Google with a [publisher restriction](../compliance/iab-tcf.md#publisher-restrictions) keeps the ad types that rest on it denied, as on the web.

## Test it

The SDK repository includes demo apps for both platforms with a verification panel that shows every stored `IABTCF_*` key and checks the setup.
