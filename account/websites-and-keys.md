---
description: Each website (or app) in Okito has its own key, banner, scans and plan.
---

# Websites and website keys

## Add a website

Open **Websites** in the dashboard and add your domain. For a mobile app, choose **Mobile app** and enter the app name, platform and bundle ID / package name.

Each website has:

* its own **website key**, used in the script URL `https://cdn.okito.com/js/YOUR_WEBSITE_KEY` (in an app, the `websiteId` of the [mobile SDK](../installation/mobile-apps.md#website-key-and-data-region)),
* its own banner, cookie scans, script blocking rules and consent records,
* its own [plan](../getting-started/plans-and-limits.md).

Switch between websites with the selector at the top of the dashboard.

## The website key

The website key (for example `eu_okito-d288cf-c0d2b7-d`) is a **public** identifier: anyone can see it in your page source. That's fine. It only loads your banner, and the banner only works on your website's domain (and its subdomains).

Different from website keys, [API keys](../developers/rest-api.md) are secrets.

## One website per domain

Use a separate Okito website for each brand or domain. Don't reuse one key on unrelated domains: scans, pageview quotas, consent records and TCF vendors would mix. Subdomains of the same site (`www.`, `shop.`) can share a key, which also lets them [share one consent choice](../banner/subdomain-consent.md).

## Staging sites and local testing

The banner only loads on the website's domain and its subdomains, so not on `localhost` or `127.0.0.1`.

* **Staging site on another domain**: add it as its own website.
* **On your own computer**: open your local site under a name within the website's domain as it is set in **Websites**. For `example.com`, point a name such as `local.example.com` to your computer in its hosts file (`127.0.0.1 local.example.com` in `/etc/hosts`, or `C:\Windows\System32\drivers\etc\hosts` on Windows) and open your site at that name, on any port. The banner then works as on your live site; choices made there go into the website's consent records and count towards its pageviews.

To check only the banner's design, use the preview in [Banner Builder](../banner/banner-builder.md).
