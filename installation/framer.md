---
description: Add Okito to a Framer site with the Okito plugin.
---

# Framer

## With the Okito plugin

1. In Framer, open the **Plugins** marketplace and add **Okito Cookie Consent**.
2. Paste your Website Key from the Okito dashboard.
3. The plugin adds `<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY" async></script>` to the end of `<head>` in your site's custom code.
4. **Publish** your site.

## By hand

Open **Site settings → General → Custom code**, paste the code from **Install banner** into **Start of `<head>` tag**, and publish.

{% hint style="info" %}
Framer custom code requires a paid Framer plan. If you use Google tags, add the Consent Mode snippet by hand at the start of `<head>` as well; the plugin only loads the Okito script.
{% endhint %}
