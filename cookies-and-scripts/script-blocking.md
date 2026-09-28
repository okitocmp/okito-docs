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
* It also holds back the embeds listed under [Embedded videos, maps and posts](#embedded-videos-maps-and-posts) (YouTube, Vimeo, Google Maps and the others there).
* Your own scripts, libraries and CDNs (jQuery, jsDelivr, cdnjs), chat, payment, other maps and video iframes, and Google tags are never held back. Google tags follow [Google Consent Mode](../google/basic-and-advanced.md).
* As soon as the Okito script starts, it takes over: your blocking rules decide, a script you allow is released at once, and the visitor's choice releases the rest. Each tag runs once.

{% hint style="info" %}
The browser may still download a tag file written in your HTML while it reads the page; the early blocker stops it from running, so it sets no cookies. To avoid the download as well, mark the tag with `type="text/plain"` (see [Mark scripts manually](manual-script-marking.md)).
{% endhint %}

## Tracking requests from your own code

Some tracking tools are bundled into a site's own JavaScript (for example Segment, Mixpanel or Amplitude installed from npm) or send pixels from inline code, so there is no tracker script for Okito to hold. Okito also holds the requests themselves: `fetch`, `navigator.sendBeacon`, `XMLHttpRequest` and image pixels to the data-collection addresses of known analytics and advertising services are not sent until the visitor consents to their category. Your own addresses are never held. Google's addresses are not on this list: in advanced consent mode Google Consent Mode governs them. In basic consent mode or with consent mode off, requests your own code sends to Google (for example to `google-analytics.com`) go out unless you add a [blocking rule](#blocking-rules) for those addresses; a blocking rule also holds requests to its addresses until the visitor consents to the rule's category.

If the visitor switched off a single service in a category, requests of that category are held unless Okito can tell they belong to another service. A pixel `<img>` written in markup (in your HTML, or added with `innerHTML`) starts loading while the browser reads the markup, before Okito can act; load such pixels from code or mark the tag that adds them instead. Pixels inside `<noscript>` never load while JavaScript runs.

With the [early blocker](#early-blocker), requests made before the Okito script starts wait: they are sent once Okito knows the visitor consented, and dropped otherwise.

## Tracking cookies

Okito keeps analytics and advertising cookies from being written before the visitor consents to their category: the ones in your [cookie list](cookie-scanner.md) and well-known tracker cookies such as `_ga`, `_fbp`, `_hj…`, `ajs_…` (Segment) and `_uet…` (Microsoft Advertising). Functional and performance cookies, and your site's other cookies, are never held by name. After a refusal Okito deletes these cookies on every domain and path of the page, and a tracker that is still running cannot write them again.

## Embedded videos, maps and posts

Embeds from these services load only after the visitor consents to their category:

| Service | Category |
| --- | --- |
| YouTube (also youtube-nocookie.com) | Advertisement |
| Vimeo | Analytics |
| Google Maps | Functional |
| Spotify | Functional |
| Dailymotion | Advertisement |
| Facebook plugins, X (Twitter) posts, TikTok | Advertisement |

Until then the visitor sees a placeholder with a **Cookie settings** button in the embed's place. Other iframes (payment, login, reCAPTCHA, chat and so on) are left alone.

An embed written in your page's HTML starts loading before the Okito script: Okito stops it and shows the placeholder, and with the [early blocker](#early-blocker) the embedded page never loads. To keep the browser from even requesting it, mark the iframe yourself (see [Mark scripts manually](manual-script-marking.md#iframes)); that also works for any other embed.

## Google tags

* **Advanced consent mode** (default): Okito does not block Google tags (gtag.js, Google Tag Manager, Google Analytics, Google Ads, including tags served through Google tag gateway). They load with the consent mode defaults and adjust when the visitor chooses. A blocking rule you add yourself still applies.
* **Basic consent mode** or **consent mode off**: Okito blocks Google tags until the visitor consents.

See [Basic and advanced consent mode](../google/basic-and-advanced.md).

{% hint style="warning" %}
Test your checkout, chat, maps and video embeds after turning script blocking on. A rule that's too broad can block something your site needs.
{% endhint %}
