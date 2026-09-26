---
description: The standard IAB APIs that ad tech and your own code can use.
---

# IAB TCF and US privacy APIs

## `__tcfapi` (IAB TCF)

Available when [IAB TCF](../compliance/iab-tcf.md) is on. Okito implements the IAB TCF CMP API (version 2.4). The TCF stub in the Consent Mode snippet and the plugins makes `__tcfapi` available before the Okito script loads; calls made then are queued.

| Command | Returns |
| --- | --- |
| `ping` | CMP status: loaded, `gdprApplies`, CMP ID (508) and version. |
| `getTCData` | The current TC data: TC string, purpose and vendor consents, legitimate interests, `enableAdvertiserConsentMode`. |
| `addEventListener` | Calls back with the TC data now and on every change (`tcloaded`, `cmpuishown`, `useractioncomplete`). |
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

Iframes can use the standard `postMessage` protocol with the `__tcfapiLocator` frame.

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
