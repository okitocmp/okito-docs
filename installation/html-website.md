---
description: Paste the Consent Mode snippet and the Okito script at the top of <head>.
---

# HTML / custom website

This is the standard installation. Every other method installs the same two pieces.

## Steps

1. In the dashboard, open **Install banner** and copy the code for your website.
2. Paste it at the **top of `<head>`** on every page, above Google Tag Manager, gtag.js and any marketing pixels.
3. Publish your site and open it in a private window to check the banner.

```html
<head>
  <!-- Optional, recommended: early blocker, the very first line (see Script blocking) -->
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>

  <!-- 1. Okito Consent Mode (only in advanced mode; copy yours from Install banner) -->
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('consent', 'default', {
      ad_storage: 'denied', ad_user_data: 'denied', ad_personalization: 'denied',
      analytics_storage: 'denied', functionality_storage: 'granted',
      personalization_storage: 'denied', security_storage: 'granted',
      region: ['AT','BE', /* … the regions where your banner asks for consent first … */ 'US'],
      wait_for_update: 500
    });
    gtag('consent', 'default', { /* granted for all other visitors */ });
    gtag('set', 'ads_data_redaction', true);
    gtag('set', 'developer_id.dZGJiMm', true);
  </script>

  <!-- 2. Okito script -->
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>

  <!-- 3. Your Google tags and other scripts come after -->
</head>
```

{% hint style="warning" %}
Always copy the snippet from **Install banner**. The example above is shortened. Your copy contains the full region list, the IAB TCF stub (when TCF can apply) and your settings for [where consent is not required](../compliance/consent-not-required.md), [ads data redaction and URL passthrough](../google/settings-reference.md).
{% endhint %}

## Why two pieces?

* The **snippet** is small and inline, so it runs before anything else. Google tags that load before the Okito script still start with the right consent state.
* The **Okito script** loads your banner, reads the visitor's choice and sends the consent mode update.

If you don't use Google tags, or you use [basic consent mode](../google/basic-and-advanced.md), you only need the Okito script. On IAB TCF sites, also keep the IAB TCF stub that **Install banner** shows at the top of `<head>`.

## `async` or not?

The Install banner code loads the Okito script without `async`, so it runs in order at the top of `<head>`. You can add `async` to save a few milliseconds of page load. Only do this if the Consent Mode snippet sits above your Google tags, because the snippet then covers the time until the Okito script runs.

## Next steps

* [Verify your installation](verify-installation.md)
* [Run a cookie scan](../cookies-and-scripts/cookie-scanner.md)
