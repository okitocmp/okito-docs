---
description: Okito is an IAB Europe registered CMP (CMP ID 508).
---

# IAB TCF

The IAB Europe Transparency & Consent Framework (TCF) is the advertising industry's standard for passing consent to ad tech vendors. Okito is a registered TCF CMP (**CMP ID 508**). It implements the CMP API version 2.4 with TCF policy version 5.

IAB TCF is included from the Standard plan.

## Turn it on

1. In Banner Builder → General, turn on **IAB TCF v2.4**.
2. Choose your vendors on the **IAB TCF** page in the dashboard. The banner shows how many partners (vendors) you work with and lists them in the preference centre.
3. Optionally turn on **Additional Consent (AC String)** and **Google ads consent from the TC string** (see [IAB TCF and Google](../google/tcf-and-google.md)).
4. Save.

## What changes on the banner

* The first layer uses IAB Europe's official text, listing the purposes, special features and the number of partners. These texts are locked in Banner Builder and translated with IAB's official translations.
* The preference centre shows purposes, special purposes, features, special features, stacks and the vendor list, including legitimate interest and the right to object.
* The visitor's choice is encoded in a **TC string**, stored in the `euconsent-v2` cookie and available through `__tcfapi`.

## Where TCF applies

TCF applies to the GDPR side of your banner. Visitors in the EEA, the UK and Switzerland always get the TCF experience on plans that include TCF. It never applies to the US State Laws template.

## For developers

* `__tcfapi` commands: `ping`, `getTCData`, `addEventListener`, `removeEventListener`. See [IAB TCF and US privacy APIs](../developers/tcf-and-usp-apis.md).
* A TCF stub is part of the Consent Mode snippet and the plugins, so `__tcfapi` exists before any vendor script runs.
* Mobile apps: the [Okito SDKs](../installation/mobile-apps.md) store the TCF keys (`IABTCF_*`) where ad SDKs read them.

## Reporting

**TCF Compliance Reporting** in the dashboard summarises TCF consent for audits.
