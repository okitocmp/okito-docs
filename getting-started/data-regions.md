---
description: You choose where Okito stores your websites, settings and consent records: Türkiye (TR) or the European Union (EU).
---

# Data regions (TR and EU)

When you create an account, you choose where its data is stored:

| Region | Website keys start with | Typical for |
| --- | --- | --- |
| **EU** | `eu_okito-…` | Businesses in the EU / EEA and most international sites |
| **TR** | `okito-…` or `tr_okito-…` | Businesses in Türkiye |

Your websites, banners, scan results, consent records and account profile are stored in that region. Sign-in at [app.okito.com](https://app.okito.com) sends you to the right region automatically.

Two shared services run in Türkiye for both regions: the sign-in directory that maps your email address to your region, and the entry point at app.okito.com and cdn.okito.com, which passes your requests on to your region.

Agencies: your account and billing are in your home region. You choose each client site's region when you add the client, and that site's data is stored there; see [Agency partners](../account/agency.md#working-with-client-websites).

The Okito script URL is always `https://cdn.okito.com/js/YOUR_WEBSITE_KEY`, whatever the region; the key tells the CDN which region to use. Apps work the same way: the [mobile SDKs](../installation/mobile-apps.md) use `https://cdn.okito.com` in both regions and send the website key with every request.

{% hint style="warning" %}
The region is fixed when the account is created. To move to another region, create a new account there and set up your websites again.
{% endhint %}
