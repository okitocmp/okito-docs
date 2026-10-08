---
description: An audit log of every consent choice.
---

# Consent records

Okito records every consent choice made in your banner. Open **Consent Management** in the dashboard.

Each record shows:

* the website,
* the visitor ID (a random identifier, not the visitor's name or email),
* the action (accept all, reject all, save preferences, opt-out),
* the categories granted,
* the date and time.

In IAB TCF mode, Okito also stores the TC string of each choice, together with the purposes, vendors and special features granted and the version of the Global Vendor List. Okito checks the TC string first: it is stored only if it is a valid IAB TC string that carries exactly the visitor's choice. Otherwise the choice is still recorded, with a note that the string was not stored.

With every choice Okito also stores what the visitor saw: the banner version, a fingerprint (SHA-256 hash) of the exact banner text shown, its language, and the time on the visitor's device. If the banner text changes, the hash changes, so you can tell which notice a visitor agreed to.

The visitor's choice applies on your site at once, also when Okito's servers cannot be reached. If a record cannot be delivered, the browser keeps it and sends it on the visitor's next page (for up to 7 days); a newer choice replaces one that is still waiting. A record that arrives late never replaces a choice the visitor made after it. Its date is the time of the choice on Okito's server clock: the time it arrived minus how long it had been waiting in the browser, so a wrong clock on the visitor's device does not change it. The device's own time is kept as a separate field.

Okito does not fingerprint the visitor's device to build the visitor ID. The visitor's IP address is stored shortened to its network (for example `203.0.113.0` instead of `203.0.113.77`), which is enough for proof without keeping the full address.

Records are listed newest first. Search by website, visitor ID or action, and choose how many rows to load per page.

Once a visitor has made a choice on a device, the preferences window on that device shows their **visitor ID** and the date of their choice, in the banner language. It is the same visitor ID as in Consent Management and on the privacy request form: if a visitor quotes it, search for it to find their records.

## Export to CSV

In Consent Management, choose a period (all records, the last 30 days, 90 days or 12 months, or **Custom dates** with a start and end date) and click **Download CSV**. The file lists one record per row, newest first, with the evidence stored for it:

* record ID, visitor ID, date (UTC) and action,
* the categories granted, the regime (GDPR, US State Laws or IAB TCF) and how the choice was made,
* country and region,
* banner ID, banner version, the hash of the notice shown and its language, and the time on the visitor's device,
* for US State Laws: Global Privacy Control, the sale and sharing opt-outs, the sensitive data choice (allowed or not, on a site that processes sensitive data; not allowed is also shown as a limit on its use) and the IAB GPP string the page gave vendors,
* for IAB TCF: the TC string (or why it was not stored), the Global Vendor List version, and the purposes and vendors,
* the shortened IP address and the browser (user agent).

An export holds at most 200,000 records, the newest first. If there are more, the end date is set to the day of the oldest record in the file: download again for the older records (records of that day are in both files). The file is UTF-8, so spreadsheet apps open it with the right characters. Every export is written to your audit log.

## Using records

* **Proof of consent**: show when and how a visitor consented, for example in a complaint or audit.
* **Privacy requests**: find a visitor's records by their visitor ID (visitors see it in the preferences window) when you handle an [access or deletion request](privacy-requests.md).

Consent records are included on every plan.

## How long records are kept

Okito keeps consent records until you set a retention period. To set one, open **Compliance → Legal basis**, add or edit a record and enter a **Retention period (days)**. From then on, the site's consent records, their history and the consent events in the audit log are deleted once they are older than that period; a check runs every hour. With several records, the longest period applies.

* **At least 400 days**: a consent is valid for 13 months, and the record is its proof. A shorter period counts as 400 days.
* **US opt-out records: at least 730 days**, as the California regulations require for records of consumer requests.
* **Kept**: privacy requests and their events. Each deletion is written to the audit log with the period, the cut-off date and the number of records deleted.

There is no legal period that fits every site: choose one that covers the time you may need to show a visitor's consent, and match your own privacy or retention policy. Records that are deleted cannot be restored. Left empty, nothing is deleted.
