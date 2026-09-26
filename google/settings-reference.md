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

**Okito:** Advanced by default. Banner Builder → General → **Google tags** → Basic sends no consent mode commands and blocks Google tags until the visitor consents. See [Basic and advanced consent mode](basic-and-advanced.md).

### `region`

**Google:** Sets the default consent state only for users in the listed regions (ISO 3166-2 country or subdivision codes). A default without `region` applies to all other users.

**Okito:** The Okito snippet sets a denied default for the regions where your banner asks for consent before tags run, and a separate default for all other visitors. Banner Builder → General → **Where consent is not required** controls whether that second default is granted or denied. With GTM you can add your own region defaults in the template.

### `wait_for_update`

**Google:** Sets how many milliseconds tags wait for a consent update command before sending data.

**Okito:** 500 ms for regions where the banner asks for consent; 0 elsewhere, or 500 ms when the browser sends a Global Privacy Control signal.

### `ads_data_redaction`

**Google:** When `ad_storage` is denied, ad click identifiers sent in network requests by Google Ads and Floodlight tags are redacted, and requests are sent through a cookieless domain.

**Okito:** On by default. Turn it off in Banner Builder → General → **Redact ads data while consent is denied**.

### `url_passthrough`

**Google:** When `ad_storage` is denied, passes ad click information (such as gclid and dclid) and other information about the ad click in the URLs of internal links, so conversions can be measured without cookies.

**Okito:** Off by default. Turn it on in Banner Builder → General → **Pass ad click information through URLs**; your internal link URLs then carry these parameters. The GTM template has the same option. On WordPress, see the [plugin filters](../installation/wordpress.md#filters-for-developers).

### `developer_id.dZGJiMm`

**Google:** A developer ID identifies the consent management platform that sets consent mode on the page.

**Okito:** Set by the snippet, the Okito script, the GTM template and the plugins.

### IAB TCF (`enableAdvertiserConsentMode`)

**Google:** On pages with an IAB TCF string, Google tags can read `ad_storage`, `ad_user_data` and `ad_personalization` from the TC string.

**Okito:** With IAB TCF on, Banner Builder → General → **Google ads consent from the TC string** sets `enableAdvertiserConsentMode`. `analytics_storage` is still sent through consent mode. See [IAB TCF and Google](tcf-and-google.md).
