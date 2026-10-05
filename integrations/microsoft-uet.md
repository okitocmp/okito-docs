---
description: Microsoft Advertising Universal Event Tracking (UET) consent mode.
---

# Microsoft Advertising (UET)

Microsoft Advertising's Universal Event Tracking (UET) tag has its own consent mode with one signal: `ad_storage`. Okito sets it for you; you don't need extra code.

## What Okito does

1.  **Default**: when the Okito script loads, it pushes a consent default to the UET queue (`window.uetq`):

    ```js
    window.uetq.push('consent', 'default', { ad_storage: 'denied' });
    ```

    Visitors outside the regions that need consent start `granted`, following your [Where consent is not required](../compliance/consent-not-required.md) setting.
2.  **Update**: when the visitor chooses, Okito pushes an update driven by the **Advertisement** category:

    ```js
    window.uetq.push('consent', 'update', { ad_storage: 'granted' }); // or 'denied'
    ```
3. Returning visitors get the update from their stored choice on every page load.

Because `uetq` is a queue that the UET tag reads when it loads, this works whether the UET tag loads before or after Okito.

## Setup

1. Keep your UET tag on the page as Microsoft provides it (in the page or through GTM).
2. Make sure your UET cookies are in the **Advertisement** category after a [cookie scan](../cookies-and-scripts/cookie-scanner.md).
3. Check it in Microsoft's UET Tag Helper browser extension: before consent the tag reports `ad_storage` denied; after **Accept All**, granted.

{% hint style="info" %}
If you also use [script blocking](../cookies-and-scripts/script-blocking.md), the UET script (`bat.bing.com`) is held until the visitor accepts Advertisement, and then starts with the granted state.
{% endhint %}
