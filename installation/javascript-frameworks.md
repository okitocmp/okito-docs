---
description: Load Okito from the root HTML document, not from a component.
---

# React, Next.js, Vue and Angular

Single-page apps change pages without reloading the HTML document. Okito must load **once**, from the root document, before your app and any Google tags. Don't add it inside a routed component: the first page (and the Google tags on it) would run without consent.

## React (Create React App, Vite)

Paste the code from **Install banner** at the top of `<head>` in `public/index.html` (Create React App) or `index.html` at the project root (Vite).

```html
<head>
  <!-- Okito Consent Mode snippet (copy from Install banner) -->
  <script>/* … */</script>
  <script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY"></script>
</head>
```

## Next.js

Use `next/script` with `strategy="beforeInteractive"` in the root layout. Inline the Consent Mode snippet with `dangerouslySetInnerHTML`.

```tsx
// app/layout.tsx (App Router)
import Script from 'next/script';

const consentMode = `/* paste the Consent Mode snippet body from Install banner */`;

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <head>
        <Script id="okito-consent-mode" strategy="beforeInteractive" dangerouslySetInnerHTML={{ __html: consentMode }} />
        <Script src="https://cdn.okito.com/js/YOUR_WEBSITE_KEY" strategy="beforeInteractive" />
      </head>
      <body>{children}</body>
    </html>
  );
}
```

With the Pages Router, add the same scripts to `pages/_document.tsx` inside `<Head>`.

## Vue and Nuxt

* **Vue (Vite)**: paste the code into `index.html` at the top of `<head>`.
* **Nuxt 3**: add the scripts to `app.head.script` in `nuxt.config.ts`:

```ts
export default defineNuxtConfig({
  app: {
    head: {
      script: [
        { innerHTML: '/* Consent Mode snippet body */', tagPriority: 'critical' },
        { src: 'https://cdn.okito.com/js/YOUR_WEBSITE_KEY', tagPriority: 'critical' },
      ],
    },
  },
});
```

## Angular

Paste the code at the top of `<head>` in `src/index.html`.

## Route changes

You don't need to do anything on route changes. The visitor's choice stays in force for the whole session, and scripts that your app adds later are handled by [script blocking](../cookies-and-scripts/script-blocking.md).
