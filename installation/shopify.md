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

### You already have an Okito account

If an Okito account already uses your store's email, the app does not add the store to it on its own. **Settings** shows **Connect to your Okito account**: choose **Email me a code**, then enter the 6-digit code from that email (it expires in 15 minutes). Nothing changes in the account until the code is entered.

### A Website Key from the Okito dashboard

You can also type a Website Key made in the Okito dashboard into **Settings**. The app accepts it when the website's domain is your store: its `myshopify.com` address, or its primary domain in Shopify (**Settings → Domains**). A store name that only looks like the website (`bestshoes.myshopify.com` for `bestshoes.com`) is not enough. That website stays on its Okito plan and billing.

## What the app does

* The theme app embed adds the Consent Mode defaults and the Okito script to your storefront, the IAB TCF stub when your banner can use IAB TCF, and the IAB GPP stub when it shows the US State Laws notice without IAB TCF.
* **Settings**: your Website Key and an on/off switch.
* **Banner Build**: change the banner from inside Shopify, or open the full Banner Builder in the Okito dashboard.
* **Shopify's Customer Privacy API**: every choice is passed to Shopify, so Shopify's own analytics and the pixels in **Settings → Customer events** follow it too. Analytics → `analytics`, advertising → `marketing` and `sale_of_data` (a US opt-out turns both off), functional → `preferences`.

{% hint style="warning" %}
Use one consent banner. If Shopify's own cookie banner (Customer Privacy) is on for the same regions, visitors see two banners. Turn Shopify's banner off where Okito covers your visitors.
{% endhint %}

## Early blocker

Turn on **Settings → Early blocker** in the Okito app to hold back tracking tags that load after the Okito app embed (Meta Pixel, TikTok, Hotjar, Microsoft Clarity, LinkedIn and others) until the visitor consents. It is off by default. Your theme, other apps' non-tracking code and Google tags are not affected; see [Early blocker](../cookies-and-scripts/script-blocking.md#early-blocker). Preview your store after turning it on.

Tags written in `layout/theme.liquid` above the app embed can still run first. To hold those too, paste the early blocker as the first line inside `<head>` in `theme.liquid`:

```html
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
```

## Without the app

You can also paste the Okito code into `layout/theme.liquid` inside `<head>` (**Online Store → Themes → Edit code**). Use either the app embed or `theme.liquid`, not both.
