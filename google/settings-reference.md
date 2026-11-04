---
description: Each consent mode setting, with Google's explanation and how Okito sets it.
---

# Consent mode settings reference

Each setting starts with Google's explanation, followed by how Okito sets it.

## Consent types

| Consent type | Google | Okito |
| --- | --- | --- |
| `ad_storage` | Enables storage, such as cookies (web) or device identifiers (apps), related to advertising. | Granted when the visitor accepts the Advertisement category, otherwise denied. |
| `ad_user_data` | Sets consent for sending user data to Google for online advertising purposes. | Granted when the visitor accepts the Advertisement category, otherwise denied. |
| `ad_personalization` | Sets consent for personalized advertising. | Granted when the visitor accepts the Advertisement category, otherwise denied. |
| `analytics_storage` | Enables storage, such as cookies (web) or app identifiers (apps), related to analytics, for example, visit duration. | Granted when the visitor accepts the Analytics category, otherwise denied. |
| `functionality_storage` | Enables storage that supports the functionality of the website or app, for example, language settings. | Granted by default; the update follows the visitor's choice for the Functional category. |
| `personalization_storage` | Enables storage related to personalization, for example, video recommendations. | Follows the visitor's choice for the Functional category. |
| `security_storage` | Enables storage related to security such as authentication functionality, fraud prevention, and other user protection. | Always granted. |

## Other settings

### Basic / advanced consent mode

**Google:** In basic consent mode, Google tags are blocked until the user interacts with a consent banner, and no data is sent to Google before that. In advanced consent mode, Google tags load when the page opens, use the default consent state, send cookieless pings while consent is denied, and send full measurement data after the user consents.

**Okito:** Advanced by default (basic on Free and Beginner). Banner Builder → General → **Google tags** → Basic blocks Google tags until the visitor consents; Okito puts the consent mode default and the visitor's choice in the data layer, so the tags read them when they load. See [Basic and advanced consent mode](basic-and-advanced.md).

### `region`

**Google:** Sets the default consent state only for users in the listed regions (ISO 3166-2 country or subdivision codes). A default without `region` applies to all other users.

**Okito:** The Okito snippet sets a denied default for the regions where your banner asks for consent before tags run, and a separate default for all other visitors. Banner Builder → General → **Where consent is not required** controls whether that second default is granted or denied. The United States is in the denied list only when US visitors get the GDPR banner: when they get the US State Laws notice (opt-out), they start granted. The WordPress plugin (from 1.1.8) and the Shopify app follow these settings on their own; copy the snippet again after you change them. With GTM you can add your own region defaults in the template.

When the snippet, the WordPress plugin or the Shopify app has set the default, the Okito script does not add a second one: Google Tag Assistant shows one default. Only when the default on the page does not match what Okito decides for the visitor (for example an older snippet that still lists the United States) does the Okito script send one consent update before the visitor chooses.

### `wait_for_update`

**Google:** Sets how many milliseconds tags wait for a consent update command before sending data.

**Okito:** 500 ms for regions where the banner asks for consent; 0 elsewhere, or 500 ms when the browser sends a Global Privacy Control signal.

With Consent Mode on, the earlier choice of a returning visitor who got the opt-in banner (not the US State Laws notice) does not wait for the Okito script: the Consent Mode snippet, the WordPress plugin, the Shopify app and the GTM template (from its next gallery release) apply it as a consent update right after the default, before any Google tag. They read the Consent Mode state the Okito script saved for that choice (`okito_gcm_state` in the browser's local storage, a necessary Okito item) and apply it only while the choice is still stored and valid for your site and the browser sends no Global Privacy Control signal; otherwise the Okito script applies the choice when it loads, as before. Copy the snippet again to get this.

### `ads_data_redaction`

**Google:** When `ad_storage` is denied, ad click identifiers sent in network requests by Google Ads and Floodlight tags are redacted, and requests are sent through a cookieless domain.

**Okito:** On by default. Turn it off in Banner Builder → General → **Redact ads data while consent is denied**.

### `url_passthrough`

**Google:** When `ad_storage` is denied, passes ad click information (such as gclid and dclid) and other information about the ad click in the URLs of internal links, so conversions can be measured without cookies.

**Okito:** Off by default. Turn it on in Banner Builder → General → **Pass ad click information through URLs**; your internal link URLs then carry these parameters. It is set with the consent mode default, before any Google tag: by the snippet (copy it again after you turn it on), the WordPress plugin (from 1.1.8) and the Shopify app. The GTM template has the same option. On WordPress, the [plugin filters](../installation/wordpress.md#filters-for-developers) still override it. Without a snippet, the Okito script sets it when it loads.

### `developer_id.dZGJiMm`

**Google:** A developer ID identifies the consent management platform that sets consent mode on the page.

**Okito:** Set by the snippet, the Okito script, the GTM template and the plugins.

### IAB TCF (`enableAdvertiserConsentMode`)

**Google:** On pages with an IAB TCF string, Google tags can read `ad_storage`, `ad_user_data` and `ad_personalization` from the TC string.

**Okito:** With IAB TCF on, Banner Builder → General → **Google ads consent from the TC string** sets `enableAdvertiserConsentMode`. `analytics_storage` is still sent through consent mode. See [IAB TCF and Google](tcf-and-google.md).
