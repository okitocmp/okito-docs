---
description: Each website (or app) in Okito has its own key, banner, scans and plan.
---

# Websites and website keys

## Add a website

Open **Websites** in the dashboard and add your domain. For a mobile app, choose **Mobile app** and enter the app name, platform and bundle ID / package name.

Each website has:

* its own **website key**, used in the script URL `https://cdn.okito.com/js/YOUR_WEBSITE_KEY`,
* its own banner, cookie scans, script blocking rules and consent records,
* its own [plan](../getting-started/plans-and-limits.md).

Switch between websites with the selector at the top of the dashboard.

## The website key

The website key (for example `eu_okito-d288cf-c0d2b7-d`) is a **public** identifier: anyone can see it in your page source. That's fine. It only loads your banner, and the banner only works on your website's domain (and its subdomains).

Different from website keys, [API keys](../developers/rest-api.md) are secrets.

## One website per domain

Use a separate Okito website for each brand or domain. Don't reuse one key on unrelated domains: scans, pageview quotas, consent records and TCF vendors would mix. Subdomains of the same site (`www.`, `shop.`) can share a key, which also lets them [share one consent choice](../banner/subdomain-consent.md).

## Staging sites

The banner only loads on the website's domain and its subdomains, and on `localhost` for local development. For a staging site on another domain, add it as its own website.
