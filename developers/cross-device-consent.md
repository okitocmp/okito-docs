---
description: Apply a signed-in user's choice on all their devices.
---

# Cross-device consent

When a visitor is signed in to your site, Okito can sync their consent choice across their devices: a choice made on the phone applies on the laptop.

## Turn it on

1. In Banner Builder → General, turn on **Cross-Device Consent** and save.
2. Tell Okito who the signed-in user is. Use any stable, opaque ID from your system (not an email address).

Before the Okito script:

```html
<script>
  window.okitoUserId = 'USER_ID'; // leave unset for anonymous visitors
</script>
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>
```

Or after the script has loaded, for example when the user logs in:

```js
OkitoCMP.identify('USER_ID');
```

On logout:

```js
OkitoCMP.identify(null);
```

## How it works

* The browser hashes the ID with SHA-256 before it leaves the page. Okito never receives your raw user ID.
* When a signed-in user makes a choice, Okito stores it for that hashed ID.
* On another device, Okito compares the stored choice with the local one; the newest wins. The visitor is told when a synced choice is applied.

In IAB TCF mode, this follows the TCF multi-device consent rules.
