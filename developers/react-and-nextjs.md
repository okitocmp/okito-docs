---
description: Add Okito to a React or Next.js site with the @okitocmp/react package.
---

# React and Next.js

The `@okitocmp/react` package puts the Okito banner on your pages and lets your components follow the visitor's choice. The banner itself (design, texts, blocking, Google Consent Mode, IAB TCF, US State Laws) is set up in Banner Builder as usual.

```bash
npm install @okitocmp/react
```

Your website key is in **Install banner**.

## Add the banner

**Next.js (App Router)**: at the top of `<head>` in `app/layout.tsx` (Pages Router: at the top of `<Head>` in `pages/_document.tsx`), in this order, as on [any site](../cookies-and-scripts/script-blocking.md): the early blocker, the **Consent Mode** snippet from **Install banner** if the page has Google tags, then the banner script. Google Tag Manager or gtag.js come after them.

```tsx
import { OkitoEarlyBlocker, OkitoScript } from '@okitocmp/react';

<head>
  <OkitoEarlyBlocker websiteKey="YOUR_WEBSITE_KEY" />
  {/* The lines inside the <script> of the Consent Mode snippet (Install banner) */}
  <script dangerouslySetInnerHTML={{ __html: CONSENT_MODE_SNIPPET }} />
  <OkitoScript websiteKey="YOUR_WEBSITE_KEY" />
  {/* Google Tag Manager / gtag.js here */}
</head>
```

Without Google tags, `<OkitoScript websiteKey="YOUR_WEBSITE_KEY" earlyBlocker />` prints the early blocker and the banner script together.

**Vite, Create React App and other browser-only apps**: put the **Install banner** snippet in the `<head>` of `index.html`, as for any HTML site: the early blocker first, the Consent Mode snippet if you use Google tags, then the banner script, all above any tags written in `index.html`. The hooks and components below work with it; you don't need `<OkitoScript>`. `<OkitoScript>` rendered in the browser adds the banner script only after your app has loaded, too late to hold Google tags or trackers written in `index.html`: use it only when `index.html` has none.

## Follow the visitor's choice

```tsx
import { useOkitoConsent, useOkitoAllowed, OkitoConsentGate } from '@okitocmp/react';

const consent = useOkitoConsent();
// { ready, hasChoice, categories: { necessary, functional, analytics, performance, advertisement, uncategorized }, services }

const analytics = useOkitoAllowed('analytics');

<OkitoConsentGate category="advertisement" fallback={<p>This video needs your consent.</p>}>
  <VideoEmbed />
</OkitoConsentGate>
```

Until the Okito script is ready, and during server rendering, only `necessary` is allowed. After that the values follow the banner and update after every choice: opt-in regions start refused; the US opt-out notice starts allowed, except with Global Privacy Control or on a site directed to minors, where every category but necessary starts refused (see [US state privacy laws](../compliance/us-state-laws.md)). `service="slug"` on a gate also checks a [service](../cookies-and-scripts/services.md) the visitor can switch off on its own.

## Cookie settings and cookie table

```tsx
import { OkitoPreferencesButton, OkitoCookieTable } from '@okitocmp/react';

<OkitoPreferencesButton />   {/* "Cookie settings": opens the preference window */}
<OkitoCookieTable />         {/* your cookie policy page: the cookies of your latest scan */}
```

## Without React

`getConsent()`, `onConsentChange(listener)`, `showPreferences()` and `identify(id, { hashed, signature })` from the same package work in any framework. They use the [JavaScript API](javascript-api.md) and the [consent events](events.md).
