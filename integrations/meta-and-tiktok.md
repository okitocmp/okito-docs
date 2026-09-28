---
description: Consent signals for the Meta (Facebook) Pixel and the TikTok Pixel.
---

# Meta and TikTok pixels

## Meta (Facebook) Pixel

If the Meta Pixel (`fbq`) is on the page, Okito sends its consent API call after every choice:

* Advertisement accepted: `fbq('consent', 'grant')`
* Advertisement refused: `fbq('consent', 'revoke')`

For the Pixel to wait for consent, call `fbq('consent', 'revoke')` before `fbq('init', …)` in your Pixel code, or let [script blocking](../cookies-and-scripts/script-blocking.md) hold the Pixel until the visitor accepts Advertisement (Okito blocks `connect.facebook.net/…/fbevents.js` by default).

### Limited Data Use (US state laws)

On the US State Laws template, when a US visitor opts out of the sale or sharing of their data (or their browser sends Global Privacy Control), Okito also sets Meta's [Limited Data Use](https://developers.facebook.com/docs/meta-pixel/implementation/data-processing-options) flag: `fbq('dataProcessingOptions', ['LDU'], 0, 0)`, with Meta working out the state. If the visitor opts in again, Okito removes the flag it set.

Meta reads the flag only before `fbq('init', …)`. Okito puts it in front of the `init` call while the Pixel's own script has not loaded yet, also for a Pixel set up after Okito (for example by Google Tag Manager). If the Pixel had already loaded before Okito, Okito still sends the flag, but Meta may not apply it to that page; the `consent` revoke above stops further events. To be sure, load the Okito script before the Pixel code.

## TikTok Pixel

If the TikTok Pixel (`ttq`) is on the page, Okito calls:

* Advertisement accepted: `ttq('enableCookie')`
* Advertisement refused: `ttq('disableCookie')`

Okito also blocks the TikTok Pixel script until the visitor accepts Advertisement.

## Other pixels

LinkedIn Insight Tag, X (Twitter) Pixel and other advertising tags have no consent API. Okito holds them back with [script blocking](../cookies-and-scripts/script-blocking.md) until the visitor accepts their category. You can also [mark them manually](../cookies-and-scripts/manual-script-marking.md).
