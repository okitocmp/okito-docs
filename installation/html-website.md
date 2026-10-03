---
description: Paste the installation code and the Consent Mode snippet at the top of <head>.
---

# HTML / custom website

This is the standard installation. The other methods install the same pieces (Google Tag Manager, Webflow and Framer without the early blocker).

## Steps

1. In the dashboard, open **Install banner** and copy the code for your website.
2. Paste it at the **top of `<head>`** on every page, above Google Tag Manager, gtag.js and any marketing pixels.
3. Publish your site and open it in a private window to check the banner.

```html
<head>
  <!-- 1. Okito early blocker: keep it the first script in <head> -->
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>

  <!-- 2. Okito Consent Mode (only in advanced mode; copy yours from Install banner) -->
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

  <!-- 3. Okito script (the rest of the installation code) -->
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>

  <!-- 4. Your Google tags and other scripts come after -->
</head>
```

{% hint style="warning" %}
Always copy the snippet from **Install banner**. The example above is shortened. Your copy contains the full region list, the IAB TCF stub (when TCF can apply), the IAB GPP stub (with the US State Laws notice, without IAB TCF) and your settings for [where consent is not required](../compliance/consent-not-required.md), [ads data redaction and URL passthrough](../google/settings-reference.md).
{% endhint %}

## What each piece does

* The **early blocker** is the first script of the installation code. Until the visitor consents, it holds back tags from known tracking services (Meta Pixel, TikTok, Hotjar, Microsoft Clarity, LinkedIn and others) that are written straight into your page. Your own scripts, libraries and Google tags are not affected. It only holds tags that come after it, so keep it the first script in `<head>`, without `async`. See [Early blocker](../cookies-and-scripts/script-blocking.md#early-blocker).
* The **snippet** is small and inline, so it runs before your Google tags. Google tags that load before the Okito script still start with the right consent state. Paste it right below the early blocker line.
* The **Okito script** loads your banner, reads the visitor's choice and sends the consent mode update.

If you don't use Google tags, or you use [basic consent mode](../google/basic-and-advanced.md), you only need the installation code (the early blocker and the Okito script). On IAB TCF sites, also keep the IAB TCF stub that **Install banner** shows, right below the early blocker line; on US State Laws sites without IAB TCF, the IAB GPP stub it shows instead.

If your site deliberately runs one of those tracking tags before consent, remove the `blocker.js` line; the Okito script works without it. Code copied from **Install banner** before the early blocker became part of it has no `blocker.js` line: paste it as the first line inside `<head>`, or copy the code again.

## `async` or not?

The Install banner code loads the Okito script without `async`, so it runs in order at the top of `<head>`. You can add `async` to the Okito script to save a few milliseconds of page load. Only do this if the Consent Mode snippet sits above your Google tags, because the snippet then covers the time until the Okito script runs. Never add `async` or `defer` to the early blocker: it only works when it runs before the page's other tags.

## Next steps

* [Verify your installation](verify-installation.md)
* [Run a cookie scan](../cookies-and-scripts/cookie-scanner.md)
