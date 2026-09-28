---
description: Fixes for the most common problems.
---

# Troubleshooting

## The banner doesn't show

1. **Is the script on the page?** View the page source and search for `cdn.okito.com/js/`. Check the key matches your website.
2. **Is an ad blocker or privacy browser active?** Turn it off, or test in a private window without extensions.
3. **Did you already choose?** The banner doesn't show again after a choice. Open a private window, or clear the site's storage.
4. **Is the domain right?** The banner only loads on the website's domain and its subdomains. Check the domain in **Websites**.
5. **Where consent is not required**: with **No banner, keep measurement on**, visitors outside the opt-in regions see no banner. Test with a VPN in an opt-in region (for example Germany).
6. **Plan limits**: if the website reached its monthly pageviews, the banner is paused until next month or an upgrade.
7. **Content-Security-Policy**: allow `https://cdn.okito.com`. See [CSP](../developers/csp-and-performance.md).

## Two banners appear

Okito is installed twice (theme + plugin + GTM), or another consent tool is active (for example Shopify's own banner or another WordPress plugin). Keep one installation and one consent tool.

## Google tags fire before consent

* Check the [load order](../google/load-order.md): the Consent Mode snippet and the Okito script must be above your Google tags.
* Open the page with `?okito_debug=1`. A yellow box names the tag that ran first. See [Debug mode](../google/debug-mode.md).
* If the tag comes from your own domain, see [Google tag gateway](../google/google-tag-gateway.md).
* In **advanced** mode Google tags load before consent by design, with a denied state; they send only cookieless pings until the visitor accepts. If you want them blocked, use [basic mode](../google/basic-and-advanced.md).

## A tag doesn't run after Accept All

* Check that its cookies are in the category the visitor accepted (Cookie Manager).
* If you [marked the script](../cookies-and-scripts/manual-script-marking.md), check `data-cookie-category` is spelled right (`necessary`, `functional`, `analytics`, `performance`, `advertisement`, or a [name used by other consent tools](../cookies-and-scripts/manual-script-marking.md) such as `marketing`).
* If a [service](../cookies-and-scripts/services.md) is switched off, its scripts stay blocked even when the category is on.

## Something on my site stopped working

A [blocking rule](../cookies-and-scripts/script-blocking.md) may be too broad. Open **Script Blocking**, find the rule that matches the script, and narrow its patterns or change it to allow the script.

## Changes in Banner Builder don't show

Click **Save Banner**, then reload your site in a private window. If you use a caching plugin or CDN that caches your HTML, clear it.

## Verify installation fails

The page must be reachable over public HTTPS, without a password, and must contain the Okito script in its HTML (not only added later by JavaScript). See [Verify your installation](../installation/verify-installation.md).

## Still stuck?

Contact [Okito support](support.md). For missing consent mode or TCF signals on Google tags, contact Okito before Google: Google support asks for proof that you contacted your CMP first.
