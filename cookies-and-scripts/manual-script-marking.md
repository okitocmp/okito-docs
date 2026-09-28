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

## Link a script to a service

To let visitors switch the script with a single [service](services.md), add `data-okito-service` with the service's slug:

```html
<script type="text/plain" data-cookie-category="analytics" data-okito-service="hotjar"
        src="https://static.hotjar.com/c/hotjar-123456.js?sv=6"></script>
```

## When to use it

* The script is written directly into your page's HTML, so it can run before Okito. The [early blocker](script-blocking.md#early-blocker) holds known trackers without marking them.
* You use [basic consent mode](../google/basic-and-advanced.md) and your Google tag is written directly in the page.
* The script's URL is too generic for a blocking rule.

A marked script runs once, when consent is given (or on each page load for visitors who already consented).
