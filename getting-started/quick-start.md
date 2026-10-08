---
description: From sign-up to a live consent banner in four steps.
---

# Quick start

## 1. Create your account

Sign up at [app.okito.com](https://app.okito.com). You enter your contact details and your website's domain, choose a plan, and choose where your data is stored (see [Data regions](data-regions.md)).

## 2. Run the setup wizard

The setup wizard opens after sign-up. It asks for:

* **Compliance template**: GDPR, US State Laws, or both. See [Consent templates](../banner/consent-templates.md).
* **Google consent mode**: keep **Enable Google Consent Mode** selected if your site uses Google Analytics, Google Ads or Google Tag Manager, and choose advanced (recommended) or basic. See [Basic and advanced consent mode](../google/basic-and-advanced.md).
* **Banner language, layout, position and theme.**

The wizard creates your banner. You can change everything later in [Banner Builder](../banner/banner-builder.md).

## 3. Install the script

The **Install banner** page shows the code for your site. For most websites, you paste two things at the top of `<head>`:

1. The **installation code**. Its first script is the [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker), which holds back tracking tags written in your page until the visitor consents; the next one is the Okito script:

```html
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>
```

2. The **Consent Mode snippet** (only if you use Google tags in advanced mode), right below the early blocker line. In basic mode on an IAB TCF site, **Install banner** shows the IAB TCF stub on its own instead (on a US State Laws site without IAB TCF, the IAB GPP stub); paste that in the same place.

Using WordPress, Shopify, Webflow, Framer or Google Tag Manager? Use the matching guide in [Installation](../installation/installation.md); those integrations add the code for you.

## 4. Check it works

1. Open your site in a private window. The banner should appear.
2. Click **Accept All**, reload, and check that the banner stays closed.
3. Add `?okito_debug=1` to the address (for example `https://example.com/?okito_debug=1`). A green box confirms the consent mode default was set before your Google tags. See [Debug mode](../google/debug-mode.md).
4. In the dashboard, run a [cookie scan](../cookies-and-scripts/cookie-scanner.md) so every cookie on your site is listed and categorised.

{% hint style="success" %}
That's it. Before sending real traffic, go through the [Go-live checklist](go-live-checklist.md).
{% endhint %}
