---
description: Any platform that lets you add code to <head> works with Okito.
---

# Other website builders and CMSs

Paste the code from **Install banner** into the platform's head code field, as early as the platform allows.

| Platform | Where to paste |
| --- | --- |
| **Wix** | Settings → Custom Code → Add Code → Head, All pages, Load code once |
| **Squarespace** | Settings → Developer tools → Code injection → Header (plan must include code injection) |
| **Magento / Adobe Commerce** | Content → Design → Configuration → HTML Head → Scripts and Style Sheets |
| **Joomla** | Your template's `index.php` inside `<head>`, or a head custom-code extension |
| **Drupal** | Your theme's `html.html.twig` inside `<head>`, or a module that adds a head script |
| **Ghost** | Settings → Code injection → Site header |
| **HubSpot CMS** | Settings → Website → Pages → Site header HTML |
| **Blogger, Weebly, Kajabi and others** | The site-wide header or tracking code field |

## Tips

* Put the Okito code **before** analytics and marketing code in the same field.
* If the platform adds its own tracking (for example built-in Google Analytics), check whether it runs before your head code. If it does, turn the built-in integration off and add those tags yourself after Okito, or through GTM.
* Some builders load custom code late. If [debug mode](../google/debug-mode.md) shows a yellow box, use [Google Tag Manager](google-tag-manager.md) with the Okito template instead. On IAB TCF sites, see [IAB TCF sites](google-tag-manager.md#iab-tcf-sites).
