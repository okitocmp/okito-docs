---
description: Add Okito to a Framer site with the Okito plugin.
---

# Framer

## With the Okito plugin

1. In Framer, open the **Plugins** marketplace and add **Okito Cookie Consent**.
2. Paste your Website Key from the Okito dashboard.
3. The plugin adds `<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY" async></script>` to the end of `<head>` in your site's custom code.
4. **Publish** your site.

The plugin doesn't add the [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker). If tracking tags (Meta Pixel, Hotjar …) are written into your site's custom code, paste only its line, not the rest of the installation code, as the first line of **Start of `<head>` tag**, above those tags:

```html
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
```

## By hand

Open **Site settings → General → Custom code**, paste the code from **Install banner** into **Start of `<head>` tag**, and publish.

{% hint style="info" %}
Framer custom code requires a paid Framer plan. If you use Google tags, add the Consent Mode snippet by hand at the start of `<head>` as well (right below the early blocker line, if you added it); the plugin only loads the Okito script.
{% endhint %}
