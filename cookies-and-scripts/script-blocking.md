---
description: Hold back tracking scripts until the visitor consents.
---

# Script blocking

Script blocking stops analytics and advertising scripts from running until the visitor allows their category (and service). When the visitor consents, Okito releases the scripts; when they refuse, the scripts never run.

Automatic blocking is on by default (the **Automatic blocking** switch in Banner Builder → General and in the Shopify app). On every plan, Okito blocks known trackers and the scripts found by your scans. Your own blocking rules are included from the Beginner plan.

If you turn **Automatic blocking** off (manual blocking), Okito asks you to confirm and then holds nothing by itself: known trackers, the scripts from your scans, tracking requests, tracking cookies, tracking storage keys and the embeds listed below load as your page loads them. What you set up yourself still holds: scripts and iframes you mark (see [Mark scripts manually](manual-script-marking.md)) and your [blocking rules](#blocking-rules), for scripts and requests. Google tags in basic consent mode or with consent mode off also still wait for consent. Cookies and tracking storage keys of a category the visitor refuses are still deleted. Choose Manual only if you hold every tag back yourself, for example with manual marking or consent settings in Google Tag Manager; the installation check (**Install banner → Verify**) reminds you that blocking is manual. If a single script breaks your site, add an allow rule for it under [Blocking rules](#blocking-rules) instead.

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
The browser may still download a tag file written in your HTML while it reads the page (browsers fetch script files they see in the page early, before any script can run); the early blocker stops it from running, so it sets no cookies, but the service receives the request. To avoid the download as well, mark the tag with `type="text/plain"` (see [Mark scripts manually](manual-script-marking.md)).

**WordPress:** with **Early blocker** on in the Okito plugin, the plugin does this for you. Before the page is sent, tags from the services above get the `type="text/plain"` marking, and preload or preconnect hints for them are removed, so they are not downloaded before consent. Page caches store the marked page. Shopify apps cannot change the theme's HTML, so on Shopify mark such tags yourself. The [tracking tag check](#tracking-tags-that-load-before-consent) lists them.
{% endhint %}

## Tracking tags that load before consent

Every [cookie scan](cookie-scanner.md) also reads your pages as your server sends them, before any script runs, and lists the tags from the tracking services above that a browser loads before the visitor chooses. Find the list in **Script Blocking** under **Tracking tags that load before consent** (in the Shopify app too), with the tag to use instead of each one. You also get an email when a scan finds a tag the previous scan did not.

* **Script tags** (`<script src="…">`): the browser downloads the file as soon as it reads the page. Replace the opening tag with the one shown, which adds `type="text/plain"` and the category, as in [Mark scripts manually](manual-script-marking.md). Okito runs it once the visitor consents.
* **Pixel images** (`<img src="…">` outside `<noscript>`): remove them, or add the pixel from a marked script.
* **Preload and preconnect hints** (`<link rel="preload">`, `preconnect`, `prefetch`, `modulepreload`) for these services: remove them. `dns-prefetch` is not listed; it only asks your visitor's DNS resolver.
* **Inline code** that adds a tracker's script: listed when no synchronous Okito script (the early blocker or the Okito script without `async`) comes before it and the scan saw your homepage contact that service before consent. Add the early blocker at the top of `<head>`, or mark the script (keep the code inside unchanged).

The check also lists the requests your homepage sent to these services before any choice was made. If a listed tag explains them, fixing that tag is enough; otherwise they come from other code, for example a Google Tag Manager tag that fires on every page.

Tags that are already marked, tags with `data-okito-ignore`, Google tags and your own scripts are never listed. Pages after the homepage are read without cookies, so a tag your server prints only after consent is not listed.

On WordPress, turn on **Early blocker** in the Okito plugin: from plugin version 1.1.5 it marks these tags for you. On Shopify, a tag added by an app embed (Themes → Customize → App embeds) cannot be edited in the theme code: turn the embed off, or use the app's own consent setting.

## Tracking requests from your own code

Some tracking tools are bundled into a site's own JavaScript (for example Segment, Mixpanel or Amplitude installed from npm) or send pixels from inline code, so there is no tracker script for Okito to hold. Okito also holds the requests themselves: `fetch`, `navigator.sendBeacon`, `XMLHttpRequest` and image pixels to the data-collection addresses of known analytics and advertising services are not sent until the visitor consents to their category. Your own addresses are never held. Google's addresses are not on this list: in advanced consent mode Google Consent Mode governs them. In basic consent mode or with consent mode off, requests your own code sends to Google (for example to `google-analytics.com`) go out unless you add a [blocking rule](#blocking-rules) for those addresses; a blocking rule also holds requests to its addresses until the visitor consents to the rule's category.

If the visitor switched off a single service in a category, requests of that category are held unless Okito can tell they belong to another service. A pixel `<img>` written in markup (in your HTML, or added with `innerHTML`) starts loading while the browser reads the markup, before Okito can act; load such pixels from code or mark the tag that adds them instead. Pixels inside `<noscript>` never load while JavaScript runs.

With the [early blocker](#early-blocker), requests made before the Okito script starts wait: they are sent once Okito knows the visitor consented, and dropped otherwise.

## Tracking cookies

Okito keeps analytics and advertising cookies from being written before the visitor consents to their category: the ones in your [cookie list](cookie-scanner.md) and well-known tracker cookies such as `_ga`, `_fbp`, `_hj…`, `ajs_…` (Segment) and `_uet…` (Microsoft Advertising). Functional and performance cookies, and your site's other cookies, are never held by name. After a refusal Okito deletes these cookies on every domain and path of the page, and a tracker that is still running cannot write them again.

The same applies to what trackers keep in the browser's storage (`localStorage` and `sessionStorage`) instead of a cookie: keys with the tracker cookie names above, the analytics and advertising keys in your cookie list, and keys trackers keep only in storage, such as Segment's `ajs_user_traits` and `ajs_group_properties`, Amplitude, PostHog, FullStory, Criteo and Klaviyo. They are not written before consent to their category, and they are deleted after a refusal. As with cookies, a key your cookie list gives as functional or performance is never held, and Okito's own keys, the IAB `IABTCF_…` keys and your site's other keys are never touched. With **Automatic blocking** off, storage writes are not held, but the keys of a refused category are still deleted.

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
