---
description: Find and categorise every cookie on your site.
---

# Cookie scanner

The cookie scanner opens your site in a real browser, visits your pages, accepts the banner (so cookies that wait for consent appear too) and lists every cookie it finds. Open it under **Cookie Manager**.

## Run a scan

1. Open **Cookie Manager** and select your website.
2. Click **Scan**. The scan takes one to three minutes.
3. Review the results: each cookie's name, domain, category, provider, duration and purpose, when known.

The scanner starts on your home page and follows links to other pages on the same domain, preferring pages like products, categories, cart, account and contact. How many pages it visits depends on your plan (5 on Free, up to 200 on Professional); see [Plans and limits](../getting-started/plans-and-limits.md).

A first scan runs automatically when you add a website.

## After a scan

* **Categories**: known cookies are categorised automatically. Check unknown ones and move them to the right category.
* **Services**: cookies from known providers are grouped into [services](services.md) (for example Google Analytics, Meta Pixel) so visitors can switch them on and off.
* **Removed cookies**: cookies from earlier scans that were not found again are archived and no longer shown in the banner.
* **Consent mode check**: each scan also checks every page for Google consent mode gaps. See [Consent mode check](../google/consent-mode-check.md).
* **Tracking tag check**: each scan also lists tracking tags in your pages that browsers load before consent, with the marked tag to use instead. See [Tracking tags that load before consent](script-blocking.md#tracking-tags-that-load-before-consent).
* **Banner update**: the banner's cookie list and the script blocking rules update right after the scan.
* **Cookie table**: the [cookie table on your cookie policy page](cookie-table.md) shows the new list.

## Scheduled scans

On the Professional plan, Okito can scan your site automatically every day, week or month. Set it in Cookie Manager under **Periodic scan**. You get an email when a scan finishes and when it finds problems.

## Add cookies by hand

If a cookie only appears behind a login or on a page the scanner can't reach, add it in Cookie Manager with its name, category, duration and description.

## Getting a complete scan

* The scanner needs your public site. It can't sign in or pass password protection.
* Scan again after you add new tags, pixels or subdomains.
* Subdomains that set different cookies (`shop.`, `blog.`) should be separate websites in Okito, or you add their cookies by hand. To [share consent across subdomains](../banner/subdomain-consent.md), keep them on one website and add their cookies by hand.
