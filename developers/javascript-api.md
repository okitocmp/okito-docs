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

// Open the preference centre (US State Laws: the opt-out pop-up),
// e.g. from a "Cookie settings" link. Also OkitoCMP.showPreferences().
window.CookieManager.showPreferences();
```

## Accept or reject from your own buttons

```js
window.cmAcceptAll();   // same as clicking "Accept All"
window.cmDeclineAll();  // same as clicking "Reject All"
```

These apply the choice like the banner buttons: consent record, consent mode update, script release and events. Because any script on the page can call them, the consent record says the choice came through the API (method `api`; on IAB TCF sites `iab-tcf`, like every TCF choice), and the choice never counts as an answer in an [A/B test](../banner/ab-testing.md).

## Identify a signed-in user

```js
// after login, with the hashed ID and signature your server made
OkitoCMP.identify('UID', { hashed: true, signature: 'SIGNATURE' });
OkitoCMP.identify(null); // after logout
```

See [Cross-device consent](cross-device-consent.md).

## Debug mode

```js
window.okitoDebug = true; // before the Okito script loads
```

Same as adding `?okito_debug=1` to the URL. See [Debug mode](../google/debug-mode.md).

## Read the visitor's consent

```js
OkitoCMP.getConsent();
// {
//   hasChoice: true,               // false before the visitor chooses
//   categories: { necessary: true, functional: false, analytics: true, performance: false, advertisement: false, uncategorized: false },
//   services: { hotjar: false }    // services switched on or off one by one
// }
```

The categories are what the banner applies now, whatever the template: opt-in regions start refused; the US opt-out notice starts allowed, except with Global Privacy Control or on a site directed to minors, where every category but necessary starts refused (see [US state privacy laws](../compliance/us-state-laws.md)). A GPC opt-out counts as a choice. `uncategorized` is the visitor's choice for the [Uncategorized](../cookies-and-scripts/cookie-categories.md) category (cookies not yet reviewed).

## React to the visitor's choice

Listen for the `okito:consent` event (every template), or `cookiemanager:consent` (GDPR banner). See [Consent events](events.md). For React and Next.js, the [@okitocmp/react](react-and-nextjs.md) package wraps this in a hook.

## Wait for the script

`OkitoCMP.getConsent()` answers once the Okito script is ready: `OkitoCMP.ready` is then `true` and the `okito:ready` event has fired on `window`. If your code may run earlier:

```js
function onOkitoReady(fn) {
  if (window.OkitoCMP && window.OkitoCMP.ready) return fn();
  window.addEventListener('okito:ready', function () { fn(); }, { once: true });
}

onOkitoReady(function () {
  if (OkitoCMP.getConsent().categories.analytics) {
    // start your own analytics
  }
});
```

## Other APIs

* IAB TCF: `__tcfapi`, and US privacy: `__uspapi`. See [IAB TCF and US privacy APIs](tcf-and-usp-apis.md).
* Google consent mode: Okito writes to `window.dataLayer` / `gtag`. Don't send your own `gtag('consent', 'update', …)` calls; they would override the visitor's choice.
