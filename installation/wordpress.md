---
description: Install the Okito Cookie Consent plugin from WordPress.org.
---

# WordPress

The **Okito Cookie Consent** plugin adds the Consent Mode defaults and the Okito script to every public page, and connects Okito to the WordPress Consent API.

## Install

1. In WordPress, open **Plugins → Add New**, search for **Okito Cookie Consent**, install and activate it.
2. Open **Okito** in the admin menu and click **Connect with Okito**. Sign in, pick your website, and the banner is enabled.
   * Prefer to do it by hand? Choose **Or set it up manually**, paste your Website Key and tick **Enable cookie consent banner on this website**.
3. Open your site in a private window to check the banner.

{% hint style="warning" %}
Don't paste the Okito script into your theme as well, and deactivate other cookie consent plugins. The plugin's Site Health check warns you if another consent plugin is active.
{% endhint %}

## What the plugin does

* **Consent Mode defaults first.** It prints the Google Consent Mode defaults (and the IAB TCF stub, when your banner can use IAB TCF) at the very top of `<head>`, before other plugins' Google tags.
* **Okito script.** It loads `https://cdn.okito.com/js/YOUR_WEBSITE_KEY` on every public page.
* **Caching and optimisation plugins.** It keeps Okito's code out of the delay, defer and combine features of WP Rocket, LiteSpeed Cache, Autoptimize, SiteGround Optimizer, W3 Total Cache and Cloudflare Rocket Loader, so consent always loads first.
* **WP Consent API.** It passes the visitor's choice to the [WP Consent API](../integrations/wp-consent-api.md), so Site Kit by Google and other compatible plugins follow it.
* **Site Health.** Under **Tools → Site Health** it checks that the banner is set up, that only one consent plugin is active, that the WP Consent API and Site Kit Consent Mode are on, and that consent defaults load before Google tags.

## Early blocker

Turn on **Okito → Settings → Early blocker** to hold back tracking tags that your theme or other plugins write into the page (Meta Pixel, TikTok, Hotjar, Microsoft Clarity, LinkedIn and others) until the visitor consents. It is off by default. Your theme, other plugins, libraries and Google tags are not affected; see [Early blocker](../cookies-and-scripts/script-blocking.md#early-blocker). Check your site after turning it on.

## Filters for developers

| Filter | Default | Use |
| --- | --- | --- |
| `okito_print_consent_mode_defaults` | `true` | Return `false` to leave out the consent mode defaults; the plugin then prints only the TCF stub (if your banner can use IAB TCF). Optional in [basic consent mode](../google/basic-and-advanced.md), where the Okito script sets the defaults; they do no harm there either. |
| `okito_consent_mode_ads_data_redaction` | `true` | Value of `ads_data_redaction` in the defaults (from version 1.1.4). |
| `okito_consent_mode_url_passthrough` | `false` | Set `url_passthrough` in the defaults (from version 1.1.4). |

```php
// In your theme's functions.php or a small plugin:
add_filter( 'okito_print_consent_mode_defaults', '__return_false' );
```

The Okito script applies your Banner Builder settings for ads data redaction and URL passthrough when it loads. The last two filters also set them in the page head, before the script loads.

## Banner design

Banner design, languages, cookie scanning and all settings stay in the Okito dashboard. The plugin's **Open Banner Builder** and **Scan Cookies** links take you there.
