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

Okito blocks scripts that are in the page when it loads and scripts that your page or tag manager adds later.

## Blocking rules

Open **Script Blocking** in the dashboard:

* **Auto-Detect from Scan** creates rules from the third-party scripts your last scan found.
* **Add Blocking Rule**: enter a name, URL patterns (comma separated, for example `google-analytics.com, gtag/js`), a category and an optional description. Scripts matching any pattern are blocked until the visitor consents to that category.

## Scripts that load before Okito

A script written directly into your page **above** the Okito script can start before Okito runs. To be safe, mark such scripts so the browser never runs them on its own; see [Mark scripts manually](manual-script-marking.md).

## Google tags

* **Advanced consent mode** (default): Okito does not block Google tags (gtag.js, Google Tag Manager, Google Analytics, Google Ads, including tags served through Google tag gateway). They load with the consent mode defaults and adjust when the visitor chooses. A blocking rule you add yourself still applies.
* **Basic consent mode** or **consent mode off**: Okito blocks Google tags until the visitor consents.

See [Basic and advanced consent mode](../google/basic-and-advanced.md).

{% hint style="warning" %}
Test your checkout, chat, maps and video embeds after turning script blocking on. A rule that's too broad can block something your site needs.
{% endhint %}
