---
description: Confirm Okito is installed correctly on your live site.
---

# Verify your installation

## 1. Verify in the dashboard

On **Install banner**, click **Verify**. Okito opens your live site and looks for the Okito script with your website key.

When the script is found, Okito also checks the order of the tags written in your page's HTML and lists what to fix:

* the Consent Mode snippet is missing or comes after Google Tag Manager or gtag.js;
* your banner uses IAB TCF but the TCF stub is missing or comes after Google tags (or the page has a stub it doesn't need);
* the [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker) is not the first script, or has `async` or `defer`;
* an optimisation plugin delays the Okito script or the Consent Mode snippet;
* the Okito script is on the page twice, or another consent tool is installed.

This check only sees the HTML: tags that Google Tag Manager or other scripts add later are not included. The [consent mode check](../google/consent-mode-check.md) and [debug mode](../google/debug-mode.md) look at what actually ran.

Verification needs a public HTTPS address. It fails on `localhost`, password-protected staging sites and sites that block unknown visitors.

## 2. Look at the banner

Open your site in a private window with ad blockers turned off:

* The banner appears.
* **Accept All**, **Reject All** and **Save preferences** close it, and it stays closed after a reload.
* The reopen button lets you change your choice.

## 3. Check the load order

Add `?okito_debug=1` to your page address. Okito shows a box in the bottom-left corner:

* **Green**: the consent mode default was set before your Google tags.
* **Yellow**: a Google tag ran first. The box explains how to fix it.

See [Debug mode](../google/debug-mode.md).

## 4. Check all your pages

Run a [cookie scan](../cookies-and-scripts/cookie-scanner.md). Every scan also runs the [consent mode check](../google/consent-mode-check.md) on each page it opens and lists any page where the Okito script is missing or a Google tag ran too early.

## Common problems

| Problem | Fix |
| --- | --- |
| No banner | Check that the script is in the page source and your ad blocker is off. See [Troubleshooting](../help/troubleshooting.md). |
| Two banners | The script is installed twice (theme + plugin + GTM), or another consent tool is active. Keep one. |
| Verify fails but the banner shows | The page Okito fetches doesn't contain the script (for example it's added only after the page loads). Put the script in the page's HTML. |
