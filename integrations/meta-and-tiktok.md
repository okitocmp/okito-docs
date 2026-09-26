---
description: Consent signals for the Meta (Facebook) Pixel and the TikTok Pixel.
---

# Meta and TikTok pixels

## Meta (Facebook) Pixel

If the Meta Pixel (`fbq`) is on the page, Okito sends its consent API call after every choice:

* Advertisement accepted: `fbq('consent', 'grant')`
* Advertisement refused: `fbq('consent', 'revoke')`

For the Pixel to wait for consent, call `fbq('consent', 'revoke')` before `fbq('init', …)` in your Pixel code, or let [script blocking](../cookies-and-scripts/script-blocking.md) hold the Pixel until the visitor accepts Advertisement (Okito blocks `connect.facebook.net/…/fbevents.js` by default).

## TikTok Pixel

If the TikTok Pixel (`ttq`) is on the page, Okito calls:

* Advertisement accepted: `ttq('enableCookie')`
* Advertisement refused: `ttq('disableCookie')`

Okito also blocks the TikTok Pixel script until the visitor accepts Advertisement.

## Other pixels

LinkedIn Insight Tag, X (Twitter) Pixel and other advertising tags have no consent API. Okito holds them back with [script blocking](../cookies-and-scripts/script-blocking.md) until the visitor accepts their category. You can also [mark them manually](../cookies-and-scripts/manual-script-marking.md).
