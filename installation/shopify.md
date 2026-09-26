---
description: Install the Okito Cookie Consent app from the Shopify App Store.
---

# Shopify

## Install

1. Install **Okito Cookie Consent** from the Shopify App Store.
2. Choose a plan. You pay through Shopify; the plans are the same as on [app.okito.com](../getting-started/plans-and-limits.md).
3. After the plan is approved, the app creates your Okito account, website, default banner and Website Key, and fills them in on the app's **Settings** page.
4. In the Shopify admin, open **Online Store → Themes → Customize → App embeds** and turn on **Okito Cookie Consent**. Save.
5. Open your storefront in a private window to check the banner.

## What the app does

* The theme app embed adds the IAB TCF stub, the Consent Mode defaults and the Okito script to your storefront.
* **Settings**: your Website Key and an on/off switch.
* **Banner Build**: change the banner from inside Shopify, or open the full Banner Builder in the Okito dashboard.

{% hint style="warning" %}
Use one consent banner. If Shopify's own cookie banner (Customer Privacy) is on for the same regions, visitors see two banners. Turn Shopify's banner off where Okito covers your visitors.
{% endhint %}

## Without the app

You can also paste the Okito code into `layout/theme.liquid` inside `<head>` (**Online Store → Themes → Edit code**). Use either the app embed or `theme.liquid`, not both.
