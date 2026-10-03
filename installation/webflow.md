---
description: Connect Webflow and Okito installs the script for you.
---

# Webflow

## With the Okito app (recommended)

1. Install the **Okito Cookie Consent** app from the Webflow Apps marketplace, or open **Webflow** in the Okito dashboard and click **Connect**.
2. Authorise the app for your Webflow site. Okito asks only for permission to read your sites and manage custom code.
3. Sign in to Okito (or create an account) and pick the Okito website that matches your Webflow site's domain.
4. Okito adds its script to your site's custom code. **Publish** your Webflow site.

The app doesn't add the [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker). If tracking tags (Meta Pixel, Hotjar …) are written into your site's custom code, paste only its line, not the rest of the installation code, as the first line of **Site settings → Custom code → Head code**, above those tags:

```html
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
```

## By hand

1. In Webflow, open **Site settings → Custom code → Head code**.
2. Paste the code from **Install banner** in the Okito dashboard.
3. Save and **Publish** the site.

Custom code requires a paid Webflow site plan.
