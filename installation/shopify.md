---
description: Install the Okito Cookie Consent app from the Shopify App Store.
---

# Shopify

## Install

1. Install **Okito Cookie Consent** from the Shopify App Store.
2. Choose where your business is located. Okito keeps your data in the matching region (the EU or Türkiye); you can't change it later.
3. Set up the banner: consent template, language, layout and position. You can change them later in **Banner Build**.
4. Choose a plan on the app's plan page in Shopify. Shopify bills it; see [Plans and billing](#plans-and-billing).
5. Once you have chosen a plan, the app creates your Okito account, website, default banner and Website Key, and fills them in on the app's **Settings** page.
6. On the app's **Settings** page, choose **Open theme editor**: it opens **App embeds** with **Cookie banner** turned on. Click **Save**. (You can also open **Online Store → Themes → Customize → App embeds** and turn it on there.)
7. In Shopify's **Customer privacy** settings, remove Shopify's own cookie banner and set the regions where Okito's banner shows; see [One consent banner](#one-consent-banner).
8. Open your storefront in a private window to check the banner.

### You already have an Okito account

If an Okito account already uses your store's email, the app does not add the store to it on its own. **Settings** shows **Confirm your Okito account**: choose **Email me a code**, then enter the 6-digit code from that email (it expires in 15 minutes) and choose **Connect store**. Nothing changes in the account until the code is entered.

The app uses the Website Key it creates for your store; **Settings** shows it, and a key made in the Okito dashboard can't be entered there.

## Plans and billing

A store connected through the app uses the app's plan in Shopify. Shopify bills it, and that plan alone decides which features the store gets, in the app and on the storefront. The plans have the limits and features listed in [Plans and limits](../getting-started/plans-and-limits.md).

* To choose or change your plan, open **Pricing** in the app's menu, or **Settings → Plan & billing → Manage plan**. Both open the app's plan page in Shopify, which lists each plan's price, limits and features.
* The app locks what your plan doesn't include, as the dashboard does: settings in Banner Build (see [Banner Build and your plan](#banner-build-and-your-plan)), **Analytics** and **TCF Reporting** (Standard), your own rules in **Script Blocking** (Beginner) and scheduled scans in **Cookie Manager** (Professional). Each lock has an **Upgrade your plan** link, which opens the app's plan page in Shopify.

### Monthly pageviews

The app's home page (**Dashboard**) and **Settings → Plan & billing** show this month's pageviews against your plan's limit, and how many are left.

* From 90% of the limit, the meter warns that the limit is close.
* When the store reaches the limit, the banner is paused until the limit resets on the 1st of next month or you choose a higher plan. The store keeps working, but no banner is shown. The meter says the banner is paused.
* Okito also emails you once that month, when the limit is reached: to the store's Okito account (your store's email, or the account you connected). Its **See your plan** button opens the app's plan page in Shopify.

### Cancel your paid plan

When you change or cancel your plan in Shopify, Okito picks up the change on its own. You don't need to open the app.

If you cancel a paid plan, Okito moves the store to Free:

* Your banner, its settings and your consent records stay. The storefront and the app use only what Free includes; see [Banner Build and your plan](#banner-build-and-your-plan).
* Free has 3,000 pageviews a month. If the store already has 3,000 or more this month, the banner is paused until the 1st of next month or you choose a higher plan.
* Okito moves the store within about 20 minutes. Until then the app's other pages show only what Free includes, while your storefront keeps the paid plan's banner settings. Opening the app's **Dashboard**, **Settings** or **Pricing** in that time opens the plan page in Shopify: choose Free there, or another plan.

## What the app does

* The **Cookie banner** app embed adds the [early blocker](#early-blocker) (unless you turn it off), the Consent Mode defaults and the Okito script to your storefront, the IAB TCF stub when your banner can use IAB TCF, and the IAB GPP stub when it shows the US State Laws notice without IAB TCF.
* **Settings**: your Website Key, an on/off switch, the early blocker, your plan and this month's [pageviews](#monthly-pageviews).
* **Banner Build**: change the banner from inside Shopify, with the dashboard's settings: texts and [links](../banner/content-and-languages.md#privacy-policy-and-kvkk-disclosure-notice-links), [Share consent across subdomains](../banner/subdomain-consent.md), [Ask every visitor again](../compliance/consent-renewal.md#ask-every-visitor-again), [Cross-Device Consent](../developers/cross-device-consent.md#shopify) with its signing key, and on the app's Professional plan the [logo and custom CSS](../banner/layout-and-position.md#logo-and-custom-css). Your plan decides which settings you can use; see [Banner Build and your plan](#banner-build-and-your-plan). With **Share consent across subdomains**, your store's `myshopify.com` address and your own domain never share a choice: browsers treat them as separate sites.
* **Cookie Manager**: your store's cookies, cookie scans, scheduled scans (Professional) and the [consent mode check](#consent-mode-check).
* **Cookie table**: a theme app block that lists your store's cookies on your cookie policy page. Add it from **Settings → Cookie table** or from the bottom of **Cookie Manager → Cookies**; see [Cookie table](../cookies-and-scripts/cookie-table.md#shopify).
* **Consent Management**: your store's [consent records](../compliance/consent-records.md).
* **Compliance Management**: [privacy requests](../compliance/privacy-requests.md), your [email notifications](#emails-from-okito) and the link to your KVKK disclosure notice (Aydınlatma Metni).
* **Shopify's Customer Privacy API**: every choice a visitor makes in the banner is passed to Shopify, so Shopify's own analytics and the pixels in **Settings → Customer events** follow it too. Analytics → `analytics`, advertising → `marketing` and `sale_of_data` (a US opt-out turns both off), functional → `preferences`. Only the visitor's own choice is passed: before a choice (the US opt-out notice, or a region where no banner is shown) Shopify's own region settings apply, as Shopify asks. A [Global Privacy Control](../compliance/us-state-laws.md#global-privacy-control-gpc) signal is applied by Okito, but it is not passed to Shopify as the visitor's choice.

## Cookie scan

When the app connects your store, Okito scans the store for cookies by itself. **Cookie Manager**, the app's **Dashboard** and **Settings** show the scan while it runs, and when it finishes (usually within a few minutes) **Cookie Manager** lists the cookies, sorted into categories and into the services your banner and script blocking use. This first scan counts as one of your monthly scans. Only one scan of your store runs at a time: while Okito's scan runs, **Scan Cookies** waits for it.

A scan that can't open your store doesn't change your cookie list and doesn't count toward your monthly scans. Cookie Manager says why, and **Scan History** shows it as **Could not scan**.

### Password-protected stores

A store with a storefront password (a development store, or a store before launch) only shows its password page, so Okito can't scan it yet. The app tells you so instead of showing the password page's few cookies as your store's.

For a store before launch:

1. In your Shopify admin, open **Online Store → Preferences**.
2. Turn off **password protection** and click **Save**.

Okito scans your store once it's open: the next time you open the app, and in the store's first days also on its own every few hours. You can also click **Scan Cookies** in **Cookie Manager**.

A development store can't remove its password: Shopify keeps it until the store moves to a paid Shopify plan. Until then Okito can't scan it; once the store is on a paid plan and its password is removed as above, click **Scan Cookies**.

## Banner Build and your plan

Banner Build locks the same settings as the dashboard's Banner Builder, by your plan in Shopify:

| Setting | Plan |
| --- | --- |
| Design themes other than Classic (**Theme** tab) | Beginner and higher |
| More than one banner language | Beginner and higher |
| The **GDPR & US State Laws** consent template | Beginner and higher |
| **No banner, keep measurement on** under **Where consent is not required** | Beginner and higher |
| **Google tags**: Advanced | Standard and higher |
| IAB TCF | Standard and higher |
| [Logo and custom CSS](../banner/layout-and-position.md#logo-and-custom-css) (**Layout** tab) | Professional |

Colours (**Colors** tab) are open on every plan, as are basic consent mode and turning consent mode off. A locked setting shows **Upgrade your plan**, which opens the app's plan page in Shopify.

When you save, a setting your plan doesn't include is saved as your plan allows: one banner language (the one you choose), the Classic theme, the banner shown where consent is not required, and basic consent mode (or off, if you chose off). IAB TCF can't be turned on below Standard; if it was on, it stays on but works only on Standard and higher. A logo and CSS saved earlier stay saved but are not shown.

**GDPR & US State Laws** on a lower plan (for example chosen in the app's setup, or kept after moving to a lower plan): the storefront doesn't pick the template by the visitor's location, but shows the one template your banner falls back to (GDPR by default, or US State Laws). When you save, Okito saves that template, and Banner Build shows it, with the message *Saved. Some settings need a higher plan and were saved as your plan allows.*

## One consent banner

Use one consent banner. If Shopify's own cookie banner stays on, visitors see two banners. In your Shopify admin:

1. Open **Settings → Customer privacy → Cookie banner**, click **⋯** and choose **Remove cookie banner**.
2. Set the regions of your custom cookie banner to every region where Okito shows its banner (see [Consent templates](../banner/consent-templates.md)). Shopify's analytics and the pixels in **Settings → Customer events** wait for the visitor's choice only in these regions: in a region that is missing, they can run before the visitor chooses.
3. Keep the **data-sharing opt-out page** and its regions for US states.

## Checkout

The Okito banner and script don't run in Shopify's checkout, so Okito doesn't hold back anything there. The visitor's choice reaches Shopify through its Customer Privacy API (see [What the app does](#what-the-app-does)).

## Early blocker

**Settings → Early blocker** in the Okito app holds back tracking tags that load after the Okito app embed (Meta Pixel, TikTok, Hotjar, Microsoft Clarity, LinkedIn and others) until the visitor consents. Your theme, other apps' non-tracking code and Google tags are not affected; see [Early blocker](../cookies-and-scripts/script-blocking.md#early-blocker).

It is on by default. The app update that made it the default turned it on once for every store, including stores where it was off. A choice you make in **Settings** after that is kept; saving **Settings** for another reason doesn't change it. To turn it off, untick **Early blocker** and click **Save settings**. Turn it off only if your store deliberately runs such a tag before consent; if you had turned it off before the update, turn it off again.

The app doesn't change your theme's code, so a tracking tag written into the theme itself, above the app embed, can still run first. **Script Blocking → Tracking tags that load before consent** in the app lists the tracking tags your cookie scans found loading before consent.

## Consent mode check

**Cookie Manager → Consent Mode** shows the [consent mode check](../google/consent-mode-check.md) for your store, on every plan. Every cookie scan checks the store's pages for a Google consent mode default set before the first Google tag. The tab shows how many pages were checked, how many have Google tags and how many have gaps, then each page's result and its fix: a setting in the app or in your Shopify admin.

| Result | Fix |
| --- | --- |
| The Okito banner did not load, or Google tags run with no consent mode default | **Open App embeds**: check that the **Cookie banner** app embed is on. If the banner did not load, also check that it is turned on in the app's **Settings**. |
| A Google tag ran before the consent mode default, or was queued before it | **Open Customer events**: add Google through the Google & YouTube app or as a custom pixel in **Settings → Customer events**; both follow your visitors' choices. If a Google tag was added to your theme outside an app, remove it where it was added. |
| Basic consent mode: a Google tag loaded before the visitor consented | **Open Customer events**: add Google through the Google & YouTube app or as a custom pixel, as above, so it waits for the visitor's choice. If a Google tag was added to your theme outside an app, remove it where it was added. |

On Free and Beginner, Google tags run in basic consent mode (unless you turn consent mode off), and the check confirms that they wait for the visitor's consent.

**Check now** runs a cookie scan of your store, which counts toward your monthly scans. Scheduled scans (Professional) run the check too.

When a scan you start (**Scan Cookies** or **Check now**) or a scheduled scan finds gaps, Okito emails the store's Okito account the affected pages with their fixes, what to do, and an **Open in Shopify admin** button that opens this tab. The email follows **Compliance alerts**; see [Emails from Okito](#emails-from-okito).

## Emails from Okito

Okito emails the store's Okito account: your store's email, or the account you connected. In the app, **Compliance Management → Settings → Email notifications** shows that address and two switches, **Scan complete** and **Compliance alerts**. They apply to every store and website on the same Okito account.

| Email | When | Switch |
| --- | --- | --- |
| Scan complete | A cookie scan of your store finishes. | **Scan complete** |
| Compliance alert | A scan finds third-party, analytics or advertising cookies. | **Compliance alerts** |
| Consent mode gaps | A scan finds [consent mode gaps](#consent-mode-check). | **Compliance alerts** |
| Tracking tags before consent | A scan finds a tracking tag or tracker request loading before consent that the last complete scan did not find. | **Compliance alerts** |
| Privacy request | A [privacy request](../compliance/privacy-requests.md) arrives, 7 days before it is due while still open, and once if it becomes overdue (up to 30 days overdue). US "Do Not Sell or Share" opt-outs send none. | **Compliance alerts** |
| Monthly pageview limit | The store reaches its plan's limit (once a month); see [Monthly pageviews](#monthly-pageviews). | None |

* To stop an email, untick its switch and click **Save preferences**. Each email names the switch that stops it.
* The pageview limit email is a service email about your store's plan. It has no switch in the app and goes out at most once a month for each store.
* Scans Okito starts by itself send no consent mode gaps or tracking tags email: the first scan of your store, and the scans after a password-protected store opens (see [Cookie scan](#cookie-scan)). The banner may not be on yet. Only **Scan Cookies**, **Check now** and scheduled scans send them.
* Weekly reports and product news are off for an account the app creates.

## Uninstall the app

* The app embed and the Cookie table block stop loading on your storefront, so the banner and the cookie table disappear.
* Okito pauses the store's website and moves it to the Free plan.
* About 48 hours later, Shopify asks Okito to erase the store's data. Okito then deletes the store's website, its consent records and its privacy requests. The Okito account the app created for the store is deleted too, unless it is still in use (for example for other websites). If you connected an existing Okito account with an email code, only the store's website and its data are deleted; the account stays.
* If you install the app again and open it before that request arrives, nothing is erased: the app checks with Shopify that it is installed on the store first.
