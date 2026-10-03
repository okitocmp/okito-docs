---
description: Load Okito from the root HTML document, not from a component.
---

# React, Next.js, Vue and Angular

Single-page apps change pages without reloading the HTML document. Okito must load **once**, from the root document, before your app and any Google tags. Don't add it inside a routed component: the first page (and the Google tags on it) would run without consent.

## React (Create React App, Vite)

Paste the code from **Install banner** at the top of `<head>` in `public/index.html` (Create React App) or `index.html` at the project root (Vite).

```html
<head>
  <!-- Okito early blocker: keep it the first script in <head> -->
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js"></script>
  <!-- Okito Consent Mode snippet (copy from Install banner) -->
  <script>/* … */</script>
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>
</head>
```

The [early blocker](../cookies-and-scripts/script-blocking.md#early-blocker) (`blocker.js`) stays the first script in `<head>`, above the Consent Mode snippet and every other tag: it only holds back tracking tags that come after it.

## Next.js

Use `next/script` with `strategy="beforeInteractive"` in the root layout. Inline the Consent Mode snippet with `dangerouslySetInnerHTML`. Put the early blocker first, as a plain `<script>`: `next/script` can load it after the tags it has to hold.

```tsx
// app/layout.tsx (App Router)
import Script from 'next/script';

const consentMode = `/* paste the Consent Mode snippet body from Install banner */`;

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <head>
        {/* Okito early blocker: keep it above every other tag you add to <head> */}
        {/* eslint-disable-next-line @next/next/no-sync-scripts */}
        <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js" />
        <Script id="okito-consent-mode" strategy="beforeInteractive" dangerouslySetInnerHTML={{ __html: consentMode }} />
        <Script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY" strategy="beforeInteractive" />
      </head>
      <body>{children}</body>
    </html>
  );
}
```

The early blocker has to be synchronous; the `eslint-disable` line keeps Next.js's `no-sync-scripts` lint rule from flagging it. In the App Router, Next.js puts its own `async` chunk files (`/_next/static/…`) above it in `<head>`: that is fine, they write no tracking tags, and Verify does not count them. `<OkitoEarlyBlocker>` from the [`@okitocmp/react`](../developers/react-and-nextjs.md) package prints the same tag.

With the Pages Router, add the same scripts to `pages/_document.tsx` inside `<Head>`, the early blocker first.

## Vue and Nuxt

* **Vue (Vite)**: paste the code into `index.html` at the top of `<head>`, in the same order as the React example.
* **Nuxt 3**: add the scripts to `app.head.script` in `nuxt.config.ts`:

```ts
export default defineNuxtConfig({
  app: {
    head: {
      script: [
        // Okito early blocker: keep it the first script in <head>
        { src: 'https://cdn.okito.com/js/YOUR_WEBSITE_KEY/blocker.js', tagPriority: 'critical' },
        { innerHTML: '/* Consent Mode snippet body */', tagPriority: 'critical' },
        { src: 'https://cdn.okito.com/js/YOUR_WEBSITE_KEY', tagPriority: 'critical' },
      ],
    },
  },
});
```

## Angular

Paste the code at the top of `<head>` in `src/index.html`, in the same order as the React example.

## Route changes

You don't need to do anything on route changes. The visitor's choice stays in force for the whole session, and scripts that your app adds later are handled by [script blocking](../cookies-and-scripts/script-blocking.md).
