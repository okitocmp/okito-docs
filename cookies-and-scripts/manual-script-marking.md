---
description: Mark scripts in your HTML so they only run after consent.
---

# Mark scripts manually

For full control, mark a script in your HTML so the browser doesn't run it on its own. Okito runs it once the visitor consents to its category.

1. Change `type` to `text/plain`.
2. Add `data-cookie-category` with the category: `necessary`, `functional`, `analytics`, `performance` or `advertisement`.

A script marked `necessary` runs as soon as the page loads, without waiting for a choice.

Markings from other consent tools also work: the `data-cookiecategory` spelling, and the category names `marketing`, `advertising`, `ads` and `targeting` (advertisement), `statistics` and `stats` (analytics), `preferences` and `functionality` (functional), `essential` and `required` (necessary). Other names are not recognised, and those scripts are not run by Okito.

A marked script always waits for consent to its category, even when its address matches no known tracker and even when a blocking rule allows that address.

```html
<!-- Before -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>

<!-- After -->
<script type="text/plain" data-cookie-category="analytics" async
        src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX"></script>
```

Inline scripts work the same way:

```html
<script type="text/plain" data-cookie-category="advertisement">
  !function(f,b,e,v,n,t,s){ /* Meta Pixel code */ }(window, document, 'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  fbq('init', 'YOUR_PIXEL_ID');
  fbq('track', 'PageView');
</script>
```

## How marked scripts run

A marked script runs once, when the visitor consents to its category (or as the page loads, for visitors who already consented). Okito puts a normal script with the same attributes and code in its place, so it runs as it would have from your page:

* Marked scripts released together run in the order they appear in the page, also when they belong to different categories.
* An inline script waits until the marked files without `async` above it have run, so an inline `lib.init()` below a marked `lib.js` finds the library. A file with `async` runs as soon as it has loaded, as it would in the page.
* A Content-Security-Policy nonce on a marked script is kept: give marked inline scripts the same `nonce` as your other scripts. Okito never turns text into code (no `eval`), so your policy needs no `'unsafe-eval'` for them.
* `onload` and load listeners on the marked script fire, errors reach `window.onerror`, and `document.currentScript` is the script itself.
* Only `type="text/plain"` holds a script back. A data block with a category, such as `<script type="application/ld+json">`, keeps its type and is never run.

## Link a script to a service

To let visitors switch the script with a single [service](services.md), add `data-okito-service` with the service's slug:

```html
<script type="text/plain" data-cookie-category="analytics" data-okito-service="hotjar"
        src="https://static.hotjar.com/c/hotjar-123456.js?sv=6"></script>
```

## Iframes

Put the address in `data-src` instead of `src` and add the category. Okito shows a placeholder and loads the iframe once the visitor consents:

```html
<iframe data-src="https://www.youtube.com/embed/VIDEO_ID" data-cookie-category="advertisement"
        width="560" height="315" data-okito-label="YouTube"></iframe>
```

`data-okito-label` is the name shown in the placeholder (optional; the embed's host name otherwise). Okito uses `data-src` only together with `data-cookie-category`: an iframe with only `data-src` (as lazy-loading plugins write it) is left to its lazy loader, and held when the loader sets its `src`. The placeholder text follows the banner language. Known embeds such as YouTube and Google Maps are held automatically too; see [Embedded videos, maps and posts](script-blocking.md#embedded-videos-maps-and-posts). Add `data-okito-ignore` to an iframe Okito must never hold.

## When to use it

* The script is written directly into your page's HTML, so it can run before Okito. The [early blocker](script-blocking.md#early-blocker) holds known trackers without marking them.
* You use [basic consent mode](../google/basic-and-advanced.md) and your Google tag is written directly in the page.
* The script's URL is too generic for a blocking rule.
