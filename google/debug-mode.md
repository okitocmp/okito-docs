---
description: Check any page of your site for consent mode load order problems.
---

# Debug mode

Open any page of your site with `?okito_debug=1` at the end of the address, for example `https://example.com/?okito_debug=1`. Okito then checks whether the consent mode default and, for IAB TCF sites, the TCF API were in place before Google tags ran. It shows the result in a box at the bottom left of the page and in the browser console.

Debug mode stays on for the browser tab. Open a page with `?okito_debug=0` to turn it off. Developers can also set `window.okitoDebug = true` before the Okito script loads.

## Green: everything is in order

![Debug mode: green](../.gitbook/assets/debug-mode-green.png)

* **The Consent Mode default was set before any Google tag.** Nothing to do.
* **No Google tag ran before Okito; Okito sets the Consent Mode default now.** Also fine.
* **The IAB TCF API (`__tcfapi`) is available to Google tags.** (TCF sites.)

## Yellow: a Google tag ran first

![Debug mode: Google Tag Manager ran first](../.gitbook/assets/debug-mode-gtm-late.png)

The box names the tag that ran too early (for example `gtag("js")` or Google Tag Manager) and tells you what to do:

1. First check whether that tag is served through [Google tag gateway](google-tag-gateway.md) (a path on your own domain). If it is, follow the Google tag gateway steps.
2. Otherwise move the Okito Consent Mode snippet and the Okito script above Google Tag Manager / gtag.js in `<head>`. See [Load order](load-order.md).

On IAB TCF sites, it also warns when Google tags ran before the TCF API was available.

## Basic mode and consent mode off

In [basic consent mode](basic-and-advanced.md), the box says Okito sends no consent mode commands and blocks Google tags until consent. When consent mode is off (by setting or plan), it says so.

## Check all pages at once

Debug mode checks one page. To check every page, use the [Consent mode check](consent-mode-check.md), which runs with each cookie scan.
