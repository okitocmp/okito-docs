---
description: Configure consent mode in the basic or the advanced configuration.
---

# Basic and advanced consent mode

Google describes two configurations:

* **Basic**: Google tags are blocked until the visitor consents, and no data is sent to Google before that.
* **Advanced**: Google tags are not blocked. They load before consent with the denied default, send cookieless pings while consent is denied, and adjust as soon as the visitor makes a choice.

Okito supports both; **advanced is the default**. Choose in Banner Builder → General → **Google tags**, or in the setup wizard.

## Advanced configuration (Google tags are not blocked)

1. In Banner Builder → General → **Google tags**, keep **Advanced: Consent Mode signals**.
2. Copy the Consent Mode snippet from **Install banner** (or Code Generator) and paste it at the top of `<head>`, followed by the Okito script, before Google Tag Manager or gtag.js. With Google Tag Manager, use the [Okito template](../installation/google-tag-manager.md) on the Consent Initialization - All Pages trigger instead (on IAB TCF sites, see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites)). The WordPress plugin and the Shopify app add both for you.
3. Leave your Google tags as they are. They load with the default consent state and receive Okito's update when the visitor chooses. Okito's [script blocking](../cookies-and-scripts/script-blocking.md) does not block Google tags in this mode.
4. Open a page with `?okito_debug=1` and check that the debug box is green (see [Debug mode](debug-mode.md)).

## Basic configuration (Google tags are blocked until consent)

1. In Banner Builder → General → **Google tags**, choose **Basic: block Google tags until consent**. Script blocking is turned on automatically. Okito puts the consent mode default and the visitor's choice in the data layer, so Google tags know the consent state when they load after consent, as Google's basic configuration expects. Nothing reaches Google before consent.
2. Keep the Okito script. The Consent Mode snippet is not needed in this configuration; it does no harm if it stays. On IAB TCF sites, keep the IAB TCF stub at the top of `<head>`: with Google tags set to basic, **Install banner** shows it on its own, and the WordPress plugin and Shopify app keep printing it. The same goes for the IAB GPP stub on US State Laws sites without IAB TCF.
3. Google tags that are added after the Okito script loads (for example by Google Tag Manager) are blocked automatically. Tags written directly in your page can run before Okito loads, so mark them: change `<script>` to `<script type="text/plain" data-cookie-category="analytics">` (use `advertisement` for Google Ads). Okito runs them once the visitor consents to that category. See [Mark scripts manually](../cookies-and-scripts/manual-script-marking.md).
4. Check it: open your site in a private window and look at the Network tab. Before consent there are no requests to googletagmanager.com or google-analytics.com; after **Accept All** the Google tags load.

## Switch back

To go back to the advanced configuration, choose **Advanced** again and make sure the Consent Mode snippet is at the top of `<head>` (on WordPress, remove the `okito_print_consent_mode_defaults` filter if you added one).

## Off

**Off: no Google consent mode** sends no consent mode commands. Google tags are then treated like any other tracker: blocked until the visitor consents to their category. On Free and Beginner plans, Google tags use basic consent mode unless you turn consent mode off; advanced is included from the Standard plan.
