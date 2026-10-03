---
description: Pick the installation method that matches your site.
---

# Choose an installation method

| Your site | Use | Guide |
| --- | --- | --- |
| Hand-coded HTML, a custom CMS or any platform that lets you edit `<head>` | Installation code (early blocker + Okito script) and the Consent Mode snippet | [HTML / custom website](html-website.md) |
| Google Tag Manager manages your tags | Okito community template in GTM | [Google Tag Manager](google-tag-manager.md) |
| WordPress | Okito Cookie Consent plugin | [WordPress](wordpress.md) |
| Shopify | Okito Cookie Consent app | [Shopify](shopify.md) |
| Webflow | Okito app for Webflow | [Webflow](webflow.md) |
| Framer | Okito plugin for Framer | [Framer](framer.md) |
| Wix, Squarespace, Magento, Joomla, Drupal, Ghost, HubSpot and others | Head code injection | [Other website builders and CMSs](other-platforms.md) |
| React, Next.js, Vue / Nuxt, Angular | Script in the root document | [React, Next.js, Vue and Angular](javascript-frameworks.md) |
| iOS or Android app | Okito mobile SDK | [iOS and Android apps](mobile-apps.md) |

## Rules for every method

1. **Install once.** Use one method per site. The script in the theme *and* a plugin *and* GTM creates two banners.
2. **Install early.** The installation code and the Consent Mode snippet belong at the top of `<head>`, before Google Tag Manager, gtag.js and marketing pixels, with the early blocker as the first script. See [Load order](../google/load-order.md).
3. **Install everywhere.** Every page and template needs the code: checkout, 404, landing pages and pages built with separate tools (for example a 3D tour or catalogue viewer).

## Where to find your code

In the dashboard, open **Install banner** for your website. It shows:

* the **installation code**: the [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker) line (`blocker.js`), which stays the first script in `<head>`, then the Okito script with your website key,
* the **Consent Mode snippet** (in advanced mode; see [Basic and advanced consent mode](../google/basic-and-advanced.md)), which goes right below the early blocker line,
* an optional **cross-device** snippet (see [Cross-device consent](../developers/cross-device-consent.md)).

The same code is under **Code Generator**.
