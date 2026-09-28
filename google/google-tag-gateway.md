---
description: How Google tag gateway affects consent, how to verify it, and what to do about a late tag.
---

# Google tag gateway (GTG)

Google tag gateway serves Google tags (gtag.js, gtm.js) and their measurement requests through a path on your own domain instead of googletagmanager.com. It does not replace consent: a tag served through GTG still needs the consent mode default before it runs and Okito's update after the visitor chooses.

GTG affects consent through load order. The Okito Consent Mode snippet and script must run before the first Google tag. A one-click setup at your CDN (for example a Google tag gateway setting in your CDN dashboard) inserts the Google tag into your pages at the edge, often at the top of `<head>`. That often prevents you from controlling the load order, so the tag can run before Okito and the consent signal arrives late.

## Check whether a tag is enrolled in GTG

1. Open your site with the browser's developer tools on the **Network** tab and reload. A tag enrolled in GTG loads from a path on your own domain (for example `https://example.com/metrics/…`) instead of `www.googletagmanager.com`, and its measurement requests go to the same path.
2. Open `https://your-domain/your-gateway-path/healthy` (for example `https://example.com/metrics/healthy`). When the gateway is set up, the page shows `ok`. This is the check described in Google's setup guide.
3. Okito [debug mode](debug-mode.md) (`?okito_debug=1`) names the Google tag that ran before the consent default. If that tag's address is on your own domain, it is served through GTG.

## Late consent signal and the tag is enrolled in GTG

We recommend **advanced consent mode (U+C)** for tags served through GTG. It is compatible with manual GTG: the tag loads with the consent state it finds, adjusts when Okito sends the update, and sends only cookieless pings while consent is denied. Choose what fits your setup:

1. **Adopt advanced consent mode (U+C)**: keep Banner Builder → General → **Google tags** on Advanced, and enable **Data Transmission Controls** and **Global Consent Defaults** in your Google tag settings according to your needs, so tags that run before Okito's update already start with the right state. If you set Global Consent Defaults for every country, keep Banner Builder → **Where consent is not required** on measurement and copy the Consent Mode snippet again.
2. **Or** move all Google tags into a Google Tag Manager container and deploy GTM through GTG. Add the [Okito GTM template](../installation/google-tag-manager.md) on the **Consent Initialization - All Pages** trigger, so Okito runs first inside the container. On IAB TCF sites, tick **My banner uses IAB TCF** in the tag (see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites)).
3. **Or** set up GTG manually (load balancer, CDN rule or server configuration) where you control the script order: the Okito Consent Mode snippet and script first in `<head>`, then the Google tag served through the gateway.

Then reload the page with `?okito_debug=1` and check that the box is green.

## Google documentation for GTG

* [Google tag gateway for advertisers](https://developers.google.com/tag-platform/tag-manager/gateway)
* [Get started with Google tag gateway](https://developers.google.com/tag-platform/tag-manager/gateway/get-started)
* [Set up Google tag gateway through your CDN](https://developers.google.com/tag-platform/tag-manager/gateway/setup-guide?setup=auto)
* [Set up Google tag gateway manually](https://developers.google.com/tag-platform/tag-manager/gateway/setup-guide?setup=manual)
* [Data transmission controls (Tag Manager Help)](https://support.google.com/tagmanager/answer/16054531)
* [Set consent defaults, including by region](https://developers.google.com/tag-platform/security/guides/consent)
