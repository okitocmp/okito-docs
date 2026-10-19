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

Older installation code that loads the script from `app.okito.com` also needs `https://app.okito.com` in `script-src`. Better, replace it with the current code from **Websites**, which loads from `cdn.okito.com`.

Example:

```
Content-Security-Policy: script-src 'self' 'nonce-RANDOM' https://cdn.okito.com https://www.googletagmanager.com; connect-src 'self' https://cdn.okito.com https://*.okito.com https://*.google-analytics.com;
```

Add the nonce to the Consent Mode snippet: `<script nonce="RANDOM">…</script>`.

Scripts you [mark](../cookies-and-scripts/manual-script-marking.md#how-marked-scripts-run) keep their nonce when Okito runs them, so give marked inline scripts the same nonce. Okito never runs code from text (no `eval`), so no `'unsafe-eval'` is needed.

## Subresource Integrity

Don't add an `integrity` hash to the Okito script. Its content changes when you save your banner, so a fixed hash would block it. The [Webflow app](../installation/webflow.md) pins a separate, versioned loader whose content never changes.

## Page speed

* The embed code loads a small language loader, which then loads your banner script (about 25 KB compressed). Both come from `cdn.okito.com`, over the same connection.
* Browsers reuse the language loader for 5 minutes, so later pages skip that request.
* The banner script holds your consent settings and depends on the visitor's region, so browsers check it for changes on each page load. When nothing changed, the check is a small "not modified" response. That is also why your banner changes appear right after you save.
* Your blocking rules and scanned scripts are built into the banner script, so they apply to the first scripts your page adds, without an extra request.
* The banner renders inside a Shadow DOM, so your site's CSS doesn't affect it and its CSS doesn't affect your site.
* The Consent Mode snippet is tiny and inline, so it adds no network request.
* Include the Okito code once. If it is included twice (for example by the theme and a plugin), the banner still loads once.

## Single-page apps

Load Okito once from the root HTML document. See [React, Next.js, Vue and Angular](../installation/javascript-frameworks.md). Scripts your app adds later are handled by [script blocking](../cookies-and-scripts/script-blocking.md).

## Ad blockers and privacy browsers

Some ad blockers and browsers (for example Brave Shields) block consent banners. That affects only those visitors; it doesn't break your setup. Test with blockers turned off.

## Caching plugins and CDNs

Don't let optimisation tools delay, defer or combine the Okito code. The WordPress plugin handles the common WordPress caching plugins for you. With Cloudflare Rocket Loader, add `data-cfasync="false"` to the Okito script tags.
