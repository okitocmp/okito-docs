---
description: The standard IAB APIs that ad tech and your own code can use.
---

# IAB TCF and US privacy APIs

## `__tcfapi` (IAB TCF)

Available when [IAB TCF](../compliance/iab-tcf.md) is on. Okito implements the IAB TCF CMP API (version 2.4). The TCF stub in the Consent Mode snippet (or on its own on **Install banner** when Google tags are set to basic or off), the plugins and the GTM template (when **My banner uses IAB TCF** is ticked) makes `__tcfapi` available before the Okito script loads; calls made then are queued. Sites whose banner cannot use IAB TCF get no stub, and `__tcfapi` is not defined for visitors in GDPR regions there. If a stub is on the page but TCF is off (for example a plan that includes TCF with TCF turned off, or the GTM template's option left ticked), queued calls are answered with `cmpStatus: "error"` and the stub is removed for visitors in GDPR regions; other visitors get `gdprApplies: false`. Google tags then follow Google Consent Mode.

| Command | Returns |
| --- | --- |
| `ping` | CMP status: loaded, `gdprApplies`, CMP ID (508) and version. |
| `getTCData` | The current TC data: TC string, purpose and vendor consents, legitimate interests, your [publisher restrictions](../compliance/iab-tcf.md#publisher-restrictions) (`publisher.restrictions`), `enableAdvertiserConsentMode`, and `addtlConsent` (the [AC string](../google/tcf-and-google.md#additional-consent), when Additional Consent is on). |
| `addEventListener` | Calls back on each step: `cmpuishown` when the banner or preferences appear, `useractioncomplete` after the visitor's choice, `tcloaded` when a stored choice is loaded. A new visitor gets `cmpuishown` first, not an empty `tcloaded`. |
| `removeEventListener` | Stops a listener. |
| `getInAppTCData` | TC data in the in-app format. |
| `getVendorList` | The Global Vendor List used by the banner. |

```js
__tcfapi('addEventListener', 2, function (tcData, success) {
  if (!success) return;
  if (tcData.eventStatus === 'tcloaded' || tcData.eventStatus === 'useractioncomplete') {
    console.log('TC string:', tcData.tcString);
    console.log('Google (vendor 755) consent:', tcData.vendor.consents[755]);
  }
});
```

Iframes can use the standard `postMessage` protocol with the `__tcfapiLocator` frame. With the GTM template, that frame appears only once the Okito script has loaded (see [Google Tag Manager](../installation/google-tag-manager.md#iab-tcf-sites)).

## `__uspapi` (US Privacy)

Available on every page. Returns the IAB US Privacy string.

```js
__uspapi('getUSPData', 1, function (data, success) {
  console.log(data.uspString); // for example "1YNN" or "1YYN" (opted out)
});
```

| Character | Meaning |
| --- | --- |
| 1 | Version |
| 2 | Notice given (`Y` / `N` / `-`) |
| 3 | Opted out of sale (`Y` / `N` / `-`) |
| 4 | Covered by the LSPA (`Y` / `N` / `-`) |

`1---` means the US Privacy string doesn't apply to the visitor.

## `__gpp` (IAB Global Privacy Platform)

GPP CMP API 1.1, for visitors who get the US State Laws notice: US visitors get the **US National section** (`usnat`, section 7), which covers every state law. Other visitors get no `__gpp`, except that a GPP stub already on the page is answered with no applicable section (`applicableSections: [-1]`) so nothing waits on it; on an IAB TCF page IAB's stub is left alone, as `__tcfapi` carries the signal there (the GTM template's `__gpp`, if its option is left ticked, is answered with no applicable section).

```js
__gpp('ping', function (data) {
  console.log(data.applicableSections); // [7] for a US visitor
  console.log(data.gppString);
});
__gpp('addEventListener', function (event) {
  if (event.eventName === 'sectionChange') console.log('new choice', event.pingData.gppString);
});
__gpp('getField', function (value) { console.log(value); }, 'usnat.SaleOptOut'); // 1 opted out, 2 not
```

| usnat field | Okito's value |
| --- | --- |
| `SharingNotice`, `SaleOptOutNotice`, `SharingOptOutNotice`, `TargetedAdvertisingOptOutNotice` | 1 (given: the notice and the **Do Not Sell or Share** link) |
| `SaleOptOut`, `SharingOptOut`, `TargetedAdvertisingOptOut` | 1 after an opt-out, with GPC, or on a site directed to minors until the visitor opts in; else 2 |
| `SensitiveDataProcessingOptOutNotice`, `SensitiveDataLimitUseNotice`, `SensitiveDataProcessing` | When the site says it processes sensitive data: notices 1, every category 1 (no consent) until the visitor allows its use, then 2. Otherwise notices and categories 0 (not applicable) |
| `KnownChildSensitiveDataConsents` | When the site is directed to minors: 1 for each age group (no consent). Otherwise 0 |
| `PersonalDataConsents` | 0 (not applicable) |
| `MspaCoveredTransaction` | 2 (no) |
| `MspaOptOutOptionMode`, `MspaServiceProviderMode` | 0 (not applicable) |
| GPC subsection | The browser's Global Privacy Control signal |

Commands: `ping`, `addEventListener`, `removeEventListener`, `hasSection`, `getSection`, `getField`. On a site with the US State Laws template (or both templates, without IAB TCF), the Consent Mode snippet (or the stub on its own on **Install banner** when Google tags are set to basic or off), the WordPress plugin and the Shopify app include IAB's GPP stub, and the GTM template adds `__gpp` when **My banner shows the US State Laws notice (IAB GPP)** is ticked, so `__gpp` exists before any ad tag runs. Iframes can use the `postMessage` protocol with the `__gppLocator` frame (with the GTM template, once the Okito script has loaded). Copy the snippet (or the stub on its own) again after switching to or from the US State Laws template or turning IAB TCF on or off; the WordPress plugin follows the change within an hour, and the Shopify app the next time you open it or save Banner Build. With the GTM template, tick or untick **My banner shows the US State Laws notice (IAB GPP)** to match. The US Privacy API (`__uspapi`) stays available alongside.
