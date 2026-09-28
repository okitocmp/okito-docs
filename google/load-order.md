---
description: Okito must run before your Google tags.
---

# Load order

For consent mode to work, the consent mode **default** must be set before the first Google tag runs. Otherwise the tag runs without consent information.

## The right order in `<head>`

```html
<head>
  <!-- 1. Okito Consent Mode snippet (sets the defaults) -->
  <script>/* from Install banner */</script>

  <!-- 2. Okito script -->
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>

  <!-- 3. Google Tag Manager / gtag.js / Google tag gateway scripts -->
  <script>(function(w,d,s,l,i){ /* GTM */ })(window,document,'script','dataLayer','GTM-XXXX');</script>

  <!-- 4. Everything else -->
</head>
```

## With Google Tag Manager

Install Okito inside GTM with the [Okito CMP template](../installation/google-tag-manager.md) on the **Consent Initialization - All Pages** trigger. GTM runs this trigger before every other tag, so the order inside the container is right. On IAB TCF sites, see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites).

## Common causes of a wrong order

| Cause | Fix |
| --- | --- |
| The Google tag is pasted above the Okito code | Move the Okito code up. |
| A plugin or theme adds Google Analytics early | Use the Okito WordPress plugin (it prints the defaults first), or turn the built-in integration off and load the tag through GTM. |
| Your CDN or host injects the Google tag (Google tag gateway) | See [Google tag gateway](google-tag-gateway.md). |
| A website builder puts custom code at the end of `<head>` | Use [Google Tag Manager](../installation/google-tag-manager.md) with the Okito template. On IAB TCF sites, see [IAB TCF sites](../installation/google-tag-manager.md#iab-tcf-sites). |

Check the order with [Debug mode](debug-mode.md): a green box means it's right.
