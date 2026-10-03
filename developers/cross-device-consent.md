---
description: Apply a signed-in user's choice on all their devices.
---

# Cross-device consent

When a visitor is signed in to your site, Okito can sync their consent choice across their devices: a choice made on the phone applies on the laptop.

## Turn it on

1. In Banner Builder → General, turn on **Cross-Device Consent** and save.
2. Copy the **cross-device signing key** that appears in Banner Builder and keep it on your server only (for example in an environment variable). Don't put it in your pages.
3. For the signed-in user, have your server make two values:
   * `uid`: the hex SHA-256 of the user's stable ID from your system,
   * `signature`: the hex HMAC-SHA256 of `uid` with the signing key.

```js
// Node.js
const crypto = require('crypto');
const uid = crypto.createHash('sha256').update(String(user.id)).digest('hex');
const signature = crypto.createHmac('sha256', process.env.OKITO_SIGNING_KEY).update(uid).digest('hex');
```

```php
// PHP
$uid = hash('sha256', (string) $user->id);
$signature = hash_hmac('sha256', $uid, getenv('OKITO_SIGNING_KEY'));
```

4. Pass them to the banner, below the early blocker and the Consent Mode snippet (if your code has one) and before the Okito script:

```html
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
<!-- the Consent Mode snippet from Install banner, if you use it -->
<script>
  window.okitoUserId = 'UID';        // leave unset for anonymous visitors
  window.okitoUserIdHashed = true;
  window.okitoUserSignature = 'SIGNATURE';
</script>
<script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>
```

Or after the script has loaded, for example when the user logs in:

```js
OkitoCMP.identify('UID', { hashed: true, signature: 'SIGNATURE' });
```

On logout:

```js
OkitoCMP.identify(null);
```

## Why the signature

Without it, anyone who guesses a user's ID (an email address or a sequential number) could read that user's choices from Okito, or record a choice in their name that their other devices would then apply. With the signature, only your server, which knows the signing key, can link a choice to a user. Okito doesn't sync or link anything without a valid signature: the choice is still recorded, for that device only.

If the key leaks, click **New key** in Banner Builder and put the new key on your server. The old key stops working within a few minutes; until your server signs with the new key, choices are not synced.

## How it works

* Okito never receives your raw user ID: only its SHA-256 hash.
* When a signed-in user makes a choice, Okito stores it for that hash.
* On another device, Okito compares the stored choice with the local one; the newest wins. The visitor is told when a synced choice is applied.
* Choices linked before signatures were required are not synced: each user's devices sync again after their next choice.

In IAB TCF mode, this follows the TCF multi-device consent rules.
