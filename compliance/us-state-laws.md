---
description: Opt-out notices, "Do Not Sell or Share" and Global Privacy Control.
---

# US state privacy laws and GPC

US state privacy laws follow an **opt-out** model: data processing can start by default, but visitors must be able to opt out of the sale and sharing of their personal data. Okito covers the 20 comprehensive state laws in force in 2026: California (CCPA / CPRA), Virginia, Colorado, Connecticut, Utah, Texas, Oregon, Montana, Florida, Iowa, Delaware, Nebraska, New Hampshire, New Jersey, Tennessee, Minnesota, Maryland, Indiana, Kentucky and Rhode Island.

## The US State Laws template

With the [US State Laws or GDPR & US State Laws template](../banner/consent-templates.md):

* US visitors see a notice at collection with a **Do Not Sell or Share My Personal Information** link.
* The link opens a pop-up where the visitor can opt out of the sale, sharing and targeted advertising of their data.
* Cookies and scripts run by default (on a site directed to minors, US visitors start opted out; see [below](#sensitive-data-and-sites-for-minors)). An opt-out turns off every category except necessary, deletes their cookies where possible and sends the denied consent mode update.

Add the same link to your site's footer. The CCPA requires it on your homepage.

## Sensitive data and sites for minors

Two settings in the banner builder's US State Laws section (in the Shopify app: **Banner Build**, US State Laws template content) follow what your site does. They also apply in the [iOS and Android apps](../installation/mobile-apps.md#us-state-privacy-laws):

* **My site processes sensitive personal information** (health, precise geolocation, racial or ethnic origin, religion, sexual orientation, biometric or genetic data and the like). Most state laws require consent before such data is used, and the CCPA lets visitors limit its use. The pop-up then asks US visitors to allow its use; until they do, it is not allowed. Without this setting the pop-up shows no sensitive data choice, as there is nothing to allow or limit. You can change the checkbox's wording in the same section.
* **My site is directed to children or teens under 16.** Several state laws require consent before a minor's data is sold or used for targeted advertising. US visitors then start opted out (only necessary cookies and scripts run) and Google consent mode starts denied for them, until they change it in the pop-up. If you added the Google Consent Mode code to your pages, copy it again from **Install banner** after changing this setting; with the [GTM template](../installation/google-tag-manager.md), untick **US visitors follow the opt-out model**. The WordPress plugin and the Shopify app already start US visitors denied until the Okito script loads.

  The pop-up choice is the visitor's own. It is not the verifiable parental consent that the CCPA and several state laws require before the data of a child under 13 is sold or shared: a site directed to children under 13 must collect that consent itself (as under COPPA).

## Global Privacy Control (GPC)

When the visitor's browser sends the [Global Privacy Control](https://globalprivacycontrol.org/) signal:

* In the US template, Okito treats it as an opt-out of sale and sharing, without the visitor having to click anything, and stores it as their choice: like any opt-out, only necessary cookies and scripts run.
* Google consent mode starts **denied** for that visitor, wherever they are.
* The US Privacy string (`__uspapi`) reports the opt-out (`1YYN`).

## Global Privacy Platform and US Privacy API

For ad tech (for example Google Ad Manager and Prebid), Okito provides:

* the IAB **Global Privacy Platform** API (`__gpp`) with the US National section (`usnat`), which carries the visitor's opt-out, their sensitive data choice and the GPC signal;
* the older IAB **US Privacy** API (`__uspapi`), kept for the tools that still read it.

The GPP string is also stored with each US consent record. See [IAB TCF and US privacy APIs](../developers/tcf-and-usp-apis.md).

## Privacy requests

US laws give residents rights to access, delete and correct their data and to appeal a refusal. The public [privacy request form](privacy-requests.md) covers these. Each request is tagged with the visitor's state law and follows its rules:

* **Response deadline**: 45 days (Iowa: 90).
* **Appeal** of a refused request: every state except California and Utah.
* **Correction**: every state except Iowa (Utah since July 2026).

In **Compliance**, California, Virginia, Colorado, Connecticut and Utah have their own pages; requests under the other laws appear under **Other US states**.

## How long records are kept

If you set a retention period for consent records, every US State Laws choice record is kept at least 24 months, as the CCPA regulations require for consumer requests, even if your site no longer shows the US notice: opt-outs, sensitive data choices and the opt-ins of visitors on a site directed to minors. Your other records follow your period, never less than 400 days (13 months of consent validity plus a margin).
