---
description: Okito is an IAB Europe registered CMP (CMP ID 508).
---

# IAB TCF

The IAB Europe Transparency & Consent Framework (TCF) is the advertising industry's standard for passing consent to ad tech vendors. Okito is a registered TCF CMP (**CMP ID 508**). It implements the CMP API version 2.4 with TCF policy version 5.

IAB TCF is included from the Standard plan.

## TCF participation

OKITO LTD participates in the IAB Europe Transparency & Consent Framework and complies with its Specifications and Policies. OKITO LTD operates Consent Management Platform with the identification number 508.

{% hint style="info" %}
Missing consent mode or TCF signals on your Google tags? Contact [Okito support](../help/support.md) first, not Google. Google support asks for proof that you contacted your CMP before it looks into consent mode questions.
{% endhint %}

## Turn it on

1. In Banner Builder → General, turn on **IAB TCF v2.4**. Turn it on if you show personalised Google ads (AdSense, Ad Manager or AdMob) to visitors in the EEA, the UK or Switzerland: Google requires a certified CMP with IAB TCF there and otherwise shows only limited ads. If scans find AdSense or Ad Manager tags on your site while TCF is off, Banner Builder reminds you.
2. Choose your vendors on the **IAB TCF** page in the dashboard. The banner shows how many partners (vendors) you work with and lists them in the preference centre. Vendors that IAB has deleted from the Global Vendor List are not offered. If one is already on your list, the page names it: the banner, the partner count and the TC string ignore it, and it is removed from your list the next time you save.
3. Optionally turn on **Additional Consent (AC String)** and **Google ads consent from the TC string** (see [IAB TCF and Google](../google/tcf-and-google.md)).
4. Save.

## What changes on the banner

* The first layer uses IAB Europe's official text, listing the purposes, special features and the number of partners. These texts are locked in Banner Builder and translated with IAB's official translations.
* While the first layer is shown, a dimmed backdrop covers the page, as the TCF Policies require (the first layer must cover all or substantially all of the page). Your banner keeps its position and colours, and keyboard focus stays in it. It is not a cookie wall: Reject all is as easy as Accept all, and the backdrop goes as soon as the visitor chooses. Banners without IAB TCF get no backdrop.
* Accept all, Reject all and Manage preferences, on the first layer and in the preference centre, get a text contrast of at least 5:1 and the same font, as the TCF Policies require. Where your colours or custom CSS fall short, the banner adjusts them as little as needed; on TCF sites Banner Builder's colour settings warn about it.
* The preference centre shows purposes, special purposes, features, special features, stacks and the vendor list, including legitimate interest and the right to object. Each purpose's vendor counts open the list of vendors behind them. A vendor's details show how long it stores data on the device (and whether that time may be refreshed) and the contents of its device storage disclosure file, which Okito reads for the visitor: their browser never contacts the vendor. It also explains that choices about vendors cover only purposes and special features: special purposes cannot be objected to, and special features may be used for Special Purpose 1 (security, fraud prevention and fixing errors) whatever the visitor chooses.
* The visitor's choice is encoded in a **TC string**, stored in the `euconsent-v2` cookie and available through `__tcfapi`. The TC string lists as disclosed exactly the vendors on your list.
* The preference centre says where the choice is stored, all on your site's own domain: the `euconsent-v2` cookie (it expires 390 days after the choice and later visits do not extend it; the banner asks again 13 calendar months after the choice, so for the few days in between the cookie is already gone and server-side readers see no TC string, never an expired one), the `cm_tcf_consent_` entry named after your domain and the `IABTCF_*` keys in local storage. With Additional Consent on, the `addtl_consent` cookie too.

## Publisher restrictions

On the **IAB TCF** page, the **Restrictions** tab limits how a vendor may use a purpose on your site:

* **Not allowed**: the vendor may not use the purpose on your site.
* **Require consent**: a purpose the vendor uses on legitimate interest needs the visitor's consent on your site.
* **Require legitimate interest**: a purpose the vendor uses with consent is based on legitimate interest on your site. Not possible for purposes 1, 3, 4, 5 and 6, where TCF never allows legitimate interest.

Restrictions apply to the vendors on your vendor list. A vendor can only have the restrictions that fit what it declares in the Global Vendor List: the two legal basis changes need a purpose the vendor marks as flexible. The dashboard offers only those. If a vendor later changes its declarations, a restriction that no longer fits is left out of the banner and the TC string.

The restrictions go into the TC string and into `getTCData` (`publisher.restrictions`), and the preference centre lists each vendor's purposes under the legal basis you require. A purpose you do not allow Google (vendor 755) counts as not accepted for `ad_storage`, `ad_user_data` and `ad_personalization` (see [IAB TCF and Google](../google/tcf-and-google.md#tcf-purposes-and-consent-mode)); for example, without purpose 3 or 4 `ad_personalization` stays denied. This applies at once, also to visitors who chose before you added the restriction. The [Okito mobile SDKs](../installation/mobile-apps.md) apply them the same way and write `IABTCF_PublisherRestrictions{ID}`. Changing restrictions asks visitors again (see below).

## When visitors are asked again

Besides after 13 months, the banner asks again when:

* you add a vendor to your vendor list that the visitor was not shown when they chose,
* you change your publisher restrictions,
* IAB updates the TCF policy version, or
* you click **Ask every visitor again** (see [Consent renewal](consent-renewal.md#ask-every-visitor-again)), or
* you turned IAB TCF on after the visitor chose on your banner without it: that choice has no TC string, so visitors GDPR applies to are asked once with the TCF banner.

Until the visitor chooses again, their earlier choice stays in effect; the new vendors have no consent until then. A choice made under an earlier TCF policy version is the exception: it is no longer valid, so it is removed (with its TC string, `IABTCF_*` keys and cookies) and the banner asks as on a first visit. So is a choice older than 13 months: its TC string, `IABTCF_*` keys and cookies are removed before vendors can read them. A routine Global Vendor List update, or removing a vendor from your list, does not ask again.

## Where TCF applies

TCF applies to the GDPR side of your banner, and only when you turn it on: no law requires IAB TCF, so with the switch off visitors in the EEA, the UK and Switzerland get the GDPR banner you wrote. It never applies to the US State Laws template.

## For developers

* `__tcfapi` commands: `ping`, `getTCData`, `addEventListener`, `removeEventListener`, `getInAppTCData` and `getVendorList`. See [IAB TCF and US privacy APIs](../developers/tcf-and-usp-apis.md).
* A TCF stub is part of the Consent Mode snippet and the plugins, so `__tcfapi` exists before any vendor script runs. With Google tags set to basic or off, **Install banner** shows the stub on its own. It is included only when your banner uses IAB TCF (TCF is on). On other sites Google tags follow Google Consent Mode instead. Copy the Consent Mode snippet (or the stub on its own) again after turning TCF on or off; the WordPress plugin follows the change within an hour, and the Shopify app the next time you open it or save Banner Build. In the GTM template, tick or untick **My banner uses IAB TCF** (see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites)).
* Mobile apps: the [Okito SDKs](../installation/mobile-apps.md) store the TCF keys (`IABTCF_*`) where ad SDKs read them.

## Reporting

**TCF Compliance Reporting** in the dashboard summarises TCF consent for audits.
