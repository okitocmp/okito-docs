---
description: Install Okito with the Okito CMP template from the GTM Community Template Gallery.
---

# Google Tag Manager

If Google Tag Manager (GTM) manages your tags, install Okito inside GTM with the **Okito CMP** template. The template sets the consent mode defaults and loads the Okito script, so you don't paste anything into your site's code.

## Add the tag

1. In GTM, open **Tags → New → Tag Configuration → Discover more tag types in the Community Template Gallery**.
2. Search for **Okito CMP**, open it and click **Add to workspace**.
3. Fill in the tag:
   * **Website Key**: copy it from the Okito dashboard (Install banner).
   * **Where consent is not required (e.g. Japan)**: use the same option as in Banner Builder (see [Where consent is not required](../compliance/consent-not-required.md)).
   * **US visitors follow the opt-out model**: tick this if your banner uses the **US State Laws** or **GDPR & US State Laws** template.
4. Trigger: **Consent Initialization - All Pages**. This trigger runs before every other tag.
5. Save, then **Submit** and publish the container.

{% hint style="danger" %}
Don't also paste the Okito script or the Consent Mode snippet into your site. With the template, GTM installs both.
{% endhint %}

## Template settings

| Setting | What it does | Default |
| --- | --- | --- |
| **Website Key** | Which Okito website to load. | — |
| **Where consent is not required** | *Keep measurement on*: visitors outside the regions that need consent start **granted**. *Measurement off until a choice*: everyone starts **denied**. | Keep measurement on |
| **US visitors follow the opt-out model** | US visitors start granted (with Global Privacy Control respected by the Okito script). Leave unticked for the GDPR template. | Off |
| **Region-specific defaults** | Your own default for specific regions (ISO 3166-1 countries or ISO 3166-2 subdivisions such as `US-CA`). A region listed here replaces the built-in default for that region. | — |
| **Wait for update** | Milliseconds GTM waits for Okito's consent update before firing tags that need consent. | 500 |
| **Redact ads data while consent is denied** | Consent mode `ads_data_redaction`. | On |
| **Pass ad click information through URLs** | Consent mode `url_passthrough`. | Off |
| **Google Developer ID** | Okito's developer ID (`dZGJiMm`). Leave as is. | dZGJiMm |

## Make your tags wait for consent

GTM needs to know which consent each tag requires:

1. Open **Admin → Container Settings** and enable **Consent Overview**.
2. In **Tags → Consent Overview** (shield icon), check each tag:
   * Google tags (GA4, Google Ads, Floodlight) have built-in consent checks. Keep them.
   * Other tags (Meta, TikTok, Hotjar …): set **Require additional consent for tag to fire** with the matching consent type, for example `ad_storage` for advertising pixels and `analytics_storage` for analytics tools.

Okito maps its categories to consent types: Advertisement → `ad_storage`, `ad_user_data`, `ad_personalization`; Analytics → `analytics_storage`; Functional → `functionality_storage`, `personalization_storage`. See the [settings reference](../google/settings-reference.md).

## Check it

Open **Preview** in GTM. In Tag Assistant, the **Consent** tab should show the default state at *Consent Initialization* and an update after you click in the banner. You can also add `?okito_debug=1` to your page URL; see [Debug mode](../google/debug-mode.md).
