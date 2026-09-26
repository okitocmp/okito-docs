---
description: Content-Security-Policy, caching, page speed and single-page apps.
---

# CSP, performance and SPAs

## Content-Security-Policy

If your site sends a Content-Security-Policy header, allow Okito:

| Directive | Add |
| --- | --- |
| `script-src` | `https://cdn.okito.com` (and `'unsafe-inline'` or a nonce/hash for the Consent Mode snippet) |
| `connect-src` | `https://cdn.okito.com https://*.okito.com` |
| `frame-src` | not needed |

Example:

```
Content-Security-Policy: script-src 'self' 'nonce-RANDOM' https://cdn.okito.com https://www.googletagmanager.com; connect-src 'self' https://cdn.okito.com https://*.okito.com https://*.google-analytics.com;
```

Add the nonce to the Consent Mode snippet: `<script nonce="RANDOM">…</script>`.

## Subresource Integrity

Don't add an `integrity` hash to the Okito script. Its content changes when you save your banner, so a fixed hash would block it.

## Page speed

* The Okito script is served from a CDN. Browsers keep a copy and check for changes on each page load; when nothing changed, the check is a small "not modified" response. That is also why your banner changes appear right after you save.
* The banner renders inside a Shadow DOM, so your site's CSS doesn't affect it and its CSS doesn't affect your site.
* The Consent Mode snippet is tiny and inline, so it adds no network request.

## Single-page apps

Load Okito once from the root HTML document. See [React, Next.js, Vue and Angular](../installation/javascript-frameworks.md). Scripts your app adds later are handled by [script blocking](../cookies-and-scripts/script-blocking.md).

## Ad blockers and privacy browsers

Some ad blockers and browsers (for example Brave Shields) block consent banners. That affects only those visitors; it doesn't break your setup. Test with blockers turned off.

## Caching plugins and CDNs

Don't let optimisation tools delay, defer or combine the Okito code. The WordPress plugin handles the common WordPress caching plugins for you. With Cloudflare Rocket Loader, add `data-cfasync="false"` to the Okito script tags.
