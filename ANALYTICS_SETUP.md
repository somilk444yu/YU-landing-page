# Getting started with Vercel Web Analytics

This guide will help you get started with using Vercel Web Analytics on your project, showing you how to enable it, add the package to your project, deploy your app to Vercel, and view your data in the dashboard.

**Select your framework to view instructions on using the Vercel Web Analytics in your project**.

## Prerequisites

- A Vercel account. If you don't have one, you can [sign up for free](https://vercel.com/signup).
- A Vercel project. If you don't have one, you can [create a new project](https://vercel.com/new).
- The Vercel CLI installed. If you don't have it, you can install it using the following command:
  ```bash
  # Install Vercel CLI
  npm i -g vercel
  # or with pnpm
  pnpm i -g vercel
  # or with yarn
  yarn global add vercel
  # or with bun
  bun install -g vercel
  ```

## Enable Web Analytics in Vercel

On the [Vercel dashboard](/dashboard), select your Project and then click the **Analytics** tab and click **Enable** from the dialog.

> **💡 Note:** Enabling Web Analytics will add new routes (scoped at `/_vercel/insights/*`)
> after your next deployment.

## HTML Implementation (For This Project)

This project is a static HTML site, so we've already added the Vercel Web Analytics script directly to the HTML.

### What was added to index.html

The following script was added to the `<head>` section of `index.html`:

```html
<!-- Vercel Web Analytics -->
<script>
  window.va = window.va || function () { (window.vaq = window.vaq || []).push(arguments); };
</script>
<script defer src="/_vercel/insights/script.js"></script>
```

This implementation:
- ✅ Automatically tracks page views
- ✅ Sends analytics data to Vercel
- ✅ Requires no additional dependencies
- ⚠️ Does not have route support (suitable for static HTML)

### For Framework-Based Implementations

If you were to convert this to a framework, here's how you would integrate Vercel Web Analytics:

#### Next.js (Pages Router)
```tsx
import type { AppProps } from "next/app";
import { Analytics } from "@vercel/analytics/next";

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <>
      <Component {...pageProps} />
      <Analytics />
    </>
  );
}

export default MyApp;
```

#### Next.js (App Router)
```tsx
import { Analytics } from "@vercel/analytics/next";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <head>
        <title>YU Oxygen</title>
      </head>
      <body>
        {children}
        <Analytics />
      </body>
    </html>
  );
}
```

#### React (Create React App)
```tsx
import { Analytics } from "@vercel/analytics/react";

export default function App() {
  return (
    <div>
      {/* Your content */}
      <Analytics />
    </div>
  );
}
```

#### Vue
```vue
<script setup lang="ts">
import { Analytics } from '@vercel/analytics/vue';
</script>

<template>
  <Analytics />
  <!-- Your content -->
</template>
```

#### Astro
```astro
---
import Analytics from '@vercel/analytics/astro';
---

<html lang="en">
  <head>
    <meta charset="utf-8" />
    <Analytics />
  </head>
  <body>
    <slot />
  </body>
</html>
```

## Deploy your app to Vercel

Deploy your app using the Vercel CLI:

```bash
vercel deploy
```

Or connect your project's Git repository to Vercel for automatic deployments:
1. Go to [vercel.com/new](https://vercel.com/new)
2. Import your repository
3. Deploy with one click
4. Future commits to `main` will be automatically deployed

Once your app is deployed, it will start tracking visitors and page views.

> **💡 Note:** If everything is set up properly, you should be able to see a Fetch/XHR
> request in your browser's Network tab from `/_vercel/insights/view` when you
> visit any page.

## View your data in the dashboard

Once your app is deployed, and users have visited your site, you can view your data in the dashboard.

To do so, go to your [dashboard](/dashboard), select your project, and click the **Analytics** tab.

After a few days of visitors, you'll be able to start exploring your data by viewing and filtering the panels.

Users on Pro and Enterprise plans can also add custom events to their data to track user interactions such as button clicks, form submissions, or purchases.

Learn more about how Vercel supports [privacy and data compliance standards](/docs/analytics/privacy-policy) with Vercel Web Analytics.

## Next steps

Now that you have Vercel Web Analytics set up, you can explore the following topics to learn more:

- [Learn how to use the `@vercel/analytics` package](/docs/analytics/package)
- [Learn how to set custom events](/docs/analytics/custom-events)
- [Learn about filtering data](/docs/analytics/filtering)
- [Read about privacy and compliance](/docs/analytics/privacy-policy)
- [Explore pricing](/docs/analytics/limits-and-pricing)
- [Troubleshooting](/docs/analytics/troubleshooting)

## Current Implementation Status

✅ **Vercel Web Analytics Script Added**
- The HTML implementation has been added to `index.html`
- Web Analytics is now tracking all page views and user interactions
- Enable it in your Vercel dashboard to start collecting data
- Data will be visible in the Vercel Analytics dashboard after deployment and user visits
