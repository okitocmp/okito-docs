---
description: Run your own code when the visitor makes or changes a choice.
---

# Consent events

## `okito:consent`

Fired on `window` after every choice, whatever the template: the GDPR banner and preference window, the US State Laws opt-out pop-up, IAB TCF, and a choice synced from another device or subdomain. `event.detail` is the same as [`OkitoCMP.getConsent()`](javascript-api.md#read-the-visitors-consent):

```js
window.addEventListener('okito:consent', function (event) {
  var consent = event.detail;
  // consent.hasChoice   -> true
  // consent.categories  -> { necessary, functional, analytics, performance, advertisement, uncategorized }
  // consent.services    -> { 'hotjar': false, ... }
});
```

## `okito:ready`

Fired on `window` once, when the Okito script is ready and the stored choice (or a Global Privacy Control opt-out) is in place; `event.detail` is `OkitoCMP.getConsent()`. Code that loads later checks `OkitoCMP.ready` instead.

## `cookiemanager:consent`

Fired on `window` every time the visitor saves a choice in the GDPR banner (Accept All, Reject All, Save preferences, or the same actions through the [JavaScript API](javascript-api.md)). Choices in the US State Laws opt-out pop-up don't fire this event; they are passed to Google consent mode and the other platforms directly.

```js
window.addEventListener('cookiemanager:consent', function (event) {
  var consent = event.detail;
  // consent.necessary      -> true
  // consent.functional     -> true / false
  // consent.analytics      -> true / false
  // consent.performance    -> true / false
  // consent.advertisement  -> true / false
  // consent.uncategorized  -> true / false
  // consent.services       -> { 'google-analytics': true, 'hotjar': false, ... }

  if (consent.analytics) {
    // start your own analytics
  }
});
```

`services` contains one entry per [service](../cookies-and-scripts/services.md), keyed by the service slug.

## `cookiemanager:tcf-consent`

Fired on `window` when a visitor saves a choice in [IAB TCF](../compliance/iab-tcf.md) mode. `event.detail` is the TC data, including the TC string. For TCF, prefer the standard `__tcfapi('addEventListener', …)`; see [IAB TCF and US privacy APIs](tcf-and-usp-apis.md).

## WordPress Consent API

On WordPress sites with the WP Consent API, Okito also calls `wp_set_consent` and fires `wp_consent_type_defined`. Plugins that use the WP Consent API receive the choice without extra code. See [WordPress Consent API](../integrations/wp-consent-api.md).

## Returning visitors

The choice events fire when a choice is **made**. For a returning visitor, their stored choice is applied when the page loads (consent mode update, script release), and `okito:ready` gives your code that state: read `OkitoCMP.getConsent()` on `okito:ready` (or at once when `OkitoCMP.ready` is `true`). You can also mark your script with a [category](../cookies-and-scripts/manual-script-marking.md) so Okito runs it only when allowed.
