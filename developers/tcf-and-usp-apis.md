---
description: The standard IAB APIs that ad tech and your own code can use.
---

# IAB TCF and US privacy APIs

## `__tcfapi` (IAB TCF)

Available when [IAB TCF](../compliance/iab-tcf.md) is on. Okito implements the IAB TCF CMP API (version 2.4). The TCF stub in the Consent Mode snippet, the plugins and the GTM template (when **My banner uses IAB TCF** is ticked) makes `__tcfapi` available before the Okito script loads; calls made then are queued. Sites whose banner cannot use IAB TCF get no stub, and `__tcfapi` is not defined for visitors in GDPR regions there. If a stub is on the page but TCF is off (for example a plan that includes TCF with TCF turned off, or the GTM template's option left ticked), queued calls are answered with `cmpStatus: "error"` and the stub is removed for visitors in GDPR regions; other visitors get `gdprApplies: false`. Google tags then follow Google Consent Mode.

| Command               | Returns                                                                                                                                                                                                                                  |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ping`                | CMP status: loaded, `gdprApplies`, CMP ID (508) and version.                                                                                                                                                                             |
| `getTCData`           | The current TC data: TC string, purpose and vendor consents, legitimate interests, `enableAdvertiserConsentMode`.                                                                                                                        |
| `addEventListener`    | Calls back on each step: `cmpuishown` when the banner or preferences appear, `useractioncomplete` after the visitor's choice, `tcloaded` when a stored choice is loaded. A new visitor gets `cmpuishown` first, not an empty `tcloaded`. |
| `removeEventListener` | Stops a listener.                                                                                                                                                                                                                        |
| `getInAppTCData`      | TC data in the in-app format.                                                                                                                                                                                                            |
| `getVendorList`       | The Global Vendor List used by the banner.                                                                                                                                                                                               |

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

| Character | Meaning                               |
| --------- | ------------------------------------- |
| 1         | Version                               |
| 2         | Notice given (`Y` / `N` / `-`)        |
| 3         | Opted out of sale (`Y` / `N` / `-`)   |
| 4         | Covered by the LSPA (`Y` / `N` / `-`) |

`1---` means the US Privacy string doesn't apply to the visitor.
