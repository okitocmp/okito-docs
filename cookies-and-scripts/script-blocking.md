---
description: Hold back tracking scripts until the visitor consents.
---

# Script blocking

Script blocking stops analytics and advertising scripts from running until the visitor allows their category (and service). When the visitor consents, Okito releases the scripts; when they refuse, the scripts never run.

Script blocking is on by default (Banner Builder → General → **Script Blocking**). On every plan, Okito blocks known trackers and the scripts found by your scans. Your own blocking rules are included from the Beginner plan.

## What gets blocked

Okito decides a script's category in this order:

1. **Your blocking rules** (below, Beginner plan and higher). A rule can also allow a script so it's never blocked.
2. **Scan results**: scripts linked to cookies found by your [cookie scans](cookie-scanner.md).
3. **Known trackers**: a built-in list of common analytics and advertising tools, including Google Analytics, Google Ads and Google Tag Manager (only in basic consent mode or when consent mode is off; see below), Meta (Facebook) Pixel, TikTok Pixel, Microsoft Advertising, LinkedIn Insight Tag, X (Twitter) Pixel, Hotjar, Matomo, Plausible and Yandex Metrica.

Necessary scripts, the Okito script itself and scripts with no known category are never blocked.

Scripts served from your own domain (your theme, jQuery, page builders, forms, sliders) run without waiting for consent, because they don't store or read tracking data. Okito holds back a script on your own domain only when it matches your rules or scan results, or when its path is clearly analytics or advertising (for example Matomo, a pixel plugin, or a Google tag served through Google tag gateway).

Okito blocks scripts that your page or tag manager adds after it has loaded. Tags written straight into your page's HTML run as the browser reads the page, before the Okito script can act: hold them back with the [early blocker](#early-blocker), or mark them yourself (see [Mark scripts manually](manual-script-marking.md)).

## Blocking rules

Open **Script Blocking** in the dashboard:

* **Auto-Detect from Scan** creates rules from the third-party scripts your last scan found.
* **Add Blocking Rule**: enter a name, URL patterns (comma separated, for example `google-analytics.com, gtag/js`), a category and an optional description. Scripts matching any pattern are blocked until the visitor consents to that category.

## Scripts that load before Okito

A script written directly into your page can run before Okito does. Use the early blocker, or mark such scripts so the browser never runs them on its own; see [Mark scripts manually](manual-script-marking.md).

## Early blocker

The early blocker holds back tracking tags written straight into your page until the visitor consents. Copy it from **Install banner** and paste it as the **very first line inside `<head>`**, above every other script, without `async`:

```html
<head>
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
  <!-- then the Consent Mode snippet, the Okito script and your other tags -->
</head>
```

* It only holds back tags from known tracking services: Meta Pixel, TikTok Pixel, Hotjar, Microsoft Clarity, LinkedIn Insight Tag, X (Twitter), Pinterest, Snap, Microsoft Advertising, Criteo, Taboola, Outbrain, The Trade Desk, Segment, Mixpanel, Amplitude, Heap, Yandex Metrica, Mouseflow, Crazy Egg, FullStory, Lucky Orange and HubSpot Analytics.
* Your own scripts, libraries and CDNs (jQuery, jsDelivr, cdnjs), chat, payment, maps, video embeds and Google tags are never held back. Google tags follow [Google Consent Mode](../google/basic-and-advanced.md).
* As soon as the Okito script starts, it takes over: your blocking rules decide, a script you allow is released at once, and the visitor's choice releases the rest. Each tag runs once.

{% hint style="info" %}
The browser may still download a tag file written in your HTML while it reads the page; the early blocker stops it from running, so it sets no cookies. To avoid the download as well, mark the tag with `type="text/plain"` (see [Mark scripts manually](manual-script-marking.md)).
{% endhint %}

## Google tags

* **Advanced consent mode** (default): Okito does not block Google tags (gtag.js, Google Tag Manager, Google Analytics, Google Ads, including tags served through Google tag gateway). They load with the consent mode defaults and adjust when the visitor chooses. A blocking rule you add yourself still applies.
* **Basic consent mode** or **consent mode off**: Okito blocks Google tags until the visitor consents.

See [Basic and advanced consent mode](../google/basic-and-advanced.md).

{% hint style="warning" %}
Test your checkout, chat, maps and video embeds after turning script blocking on. A rule that's too broad can block something your site needs.
{% endhint %}
