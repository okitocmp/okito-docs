---
description: Control the banner from your own code.
---

# JavaScript API

The Okito script exposes a small API on `window` once it has loaded.

## Open and close the banner

```js
// Show the banner again, e.g. from a "Cookie settings" link
window.CookieManager.forceShowBanner();

// Hide the banner
window.CookieManager.hideBanner();
```

## Accept or reject from your own buttons

```js
window.cmAcceptAll();   // same as clicking "Accept All"
window.cmDeclineAll();  // same as clicking "Reject All"
```

These record the choice exactly like the banner buttons: consent records, consent mode update, script release and events.

## Identify a signed-in user

```js
OkitoCMP.identify('USER_ID'); // after login
OkitoCMP.identify(null);      // after logout
```

See [Cross-device consent](cross-device-consent.md).

## Debug mode

```js
window.okitoDebug = true; // before the Okito script loads
```

Same as adding `?okito_debug=1` to the URL. See [Debug mode](../google/debug-mode.md).

## React to the visitor's choice

Listen for the `cookiemanager:consent` event. See [Consent events](events.md).

## Wait for the script

The API exists once the Okito script has run. If your code may run earlier, check first:

```js
function onOkitoReady(fn) {
  if (window.CookieManager && window.cmAcceptAll) return fn();
  setTimeout(function () { onOkitoReady(fn); }, 100);
}

onOkitoReady(function () {
  document.querySelector('#cookie-settings').addEventListener('click', function (e) {
    e.preventDefault();
    window.CookieManager.forceShowBanner();
  });
});
```

## Other APIs

* IAB TCF: `__tcfapi`, and US privacy: `__uspapi`. See [IAB TCF and US privacy APIs](tcf-and-usp-apis.md).
* Google consent mode: Okito writes to `window.dataLayer` / `gtag`. Don't send your own `gtag('consent', 'update', …)` calls; they would override the visitor's choice.
