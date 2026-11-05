---
description: Connect Webflow and Okito installs the script for you.
---

# Webflow

## With the Okito app (recommended)

1. Install the **Okito Cookie Consent** app from the Webflow Apps marketplace (or open it from your site in Webflow).
2. Sign in to Okito, or create a free account. Webflow then asks you to authorise Okito for your site. Okito asks only for permission to read your sites and manage custom code.
3. Okito shows the site you authorised. If an Okito website with the same domain exists, click **Connect**; otherwise choose your country or region and Okito creates the website for you. If you authorised several sites, pick the one to set up: nothing is chosen for you.
4. Okito adds its script to your site's custom code. **Publish** your Webflow site.

Starting from the Okito dashboard works too: open **Webflow**, choose the project and click **Connect Webflow**.

**A second Webflow site.** Install the app on that site too; your first site stays connected. Each Okito website has its own plan: your account's free website is used by the first one, so a second website needs a paid plan, which you choose right there (see [Plans and limits](../getting-started/plans-and-limits.md)). Your Webflow authorisation is kept while you pay, so you can come back and finish later.

**Opening the app again** (from the Apps panel, Site settings or the marketplace) shows your connected sites and their script status. You don't have to authorise Okito again.

The app adds one small loader, `https://cdn.okito.com/wf/1.0.0/YOUR_WEBSITE_KEY.js`, which loads your Okito script. Webflow pins it with an integrity (SRI) hash under version `1.0.0`. The loader is the same for every site and never changes, so changes to your banner (texts, languages, an [A/B test](../banner/ab-testing.md)) and Okito updates apply without applying the script again or publishing.

**Connected your site before the loader?** Then the app registered the Okito script itself (`/js/YOUR_WEBSITE_KEY`), whose pinned hash stops matching when your banner settings change or Okito updates, and the browser then refuses to load the banner. Switch once: open **Webflow** in the Okito dashboard, click **Update Okito script**, then **Publish** your Webflow site.

The app doesn't add the [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker). If tracking tags (Meta Pixel, Hotjar …) are written into your site's custom code, paste only its line, not the rest of the installation code, as the first line of **Site settings → Custom code → Head code**, above those tags:

```html
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
```

## By hand

1. In Webflow, open **Site settings → Custom code → Head code**.
2. Paste the code from **Install banner** in the Okito dashboard.
3. Save and **Publish** the site.

Custom code requires a paid Webflow site plan.

## Remove Okito

**Installed with the app**

Follow these steps in order. Uninstalling the app does not take Okito's script off your site: if you uninstall first, Okito can't reach the site any more, and the script and the banner stay on the published site.

1. In the Okito dashboard, open **Webflow** and click **Disconnect**. Okito removes its script from your site's custom code and unlinks the Okito website. Okito stays authorised in Webflow, so you can connect the site again later without authorising it again.
2. If you pasted the early blocker line by hand, delete it from **Site settings → Custom code → Head code**.
3. **Publish** your Webflow site. Until you publish, the live site keeps the banner.
4. To remove Okito's access to your site completely, uninstall the **Okito Cookie Consent** app in Webflow (**Site settings → Apps & integrations**). Okito then deletes its access to the site.

**If you uninstalled the app first**

Okito shows the site as **Needs authorization**, and the banner keeps showing. Click **Authorize again**, then follow the steps above. Don't click **Disconnect** before you authorise again: Okito can't reach the site, so the script stays, and the site leaves your list. If that happened, connect the site to Okito again, then follow the steps above. To stop the banner without authorising again, turn the website off on the **Websites** page in Okito.

**Installed by hand**

Delete the Okito code (and the early blocker line, if you added it) from **Site settings → Custom code → Head code**, save and **Publish** the site.

Removing the script from your site doesn't delete your Okito website or its consent records; delete the website in the Okito dashboard if you no longer need them.
