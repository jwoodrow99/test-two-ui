# Test Two UI

This is the PrismLabs UI component library base on shadcn ui for svelte.

## Usage

This library was built with SvelteKit and has been tested in a SvelteKit project. We provide instructions from creating a compatible SvelteKit project and configuring it as an SPA, which is primarily how we develop our client interfaces for our web applications.

### Create project

We will be using the ```sv``` tool to create a basic Svelte Kit project with the following configuration options.

``` sh
npx sv create <project_name>

┌  Welcome to the Svelte CLI! (v0.9.11)
│
◇  Which template would you like?
│  SvelteKit minimal
│
◇  Add type checking with TypeScript?
│  Yes, using TypeScript syntax
│
◆  Project created
│
◇  What would you like to add to your project? (use arrow keys / space bar)
│  tailwindcss, sveltekit-adapter
│
◇  tailwindcss: Which plugins would you like to add?
│  typography, forms
│
◇  sveltekit-adapter: Which SvelteKit adapter would you like to use?
│  static
│
◆  Successfully setup add-ons
│
◇  Which package manager do you want to install dependencies with?
│  npm
│
◆  Successfully installed dependencies# Install dependencies
└  You're all set!
```

### Configure as SPA

By default SvelteKit will assume you want the project to use SSR, You will need to create a ```+layout.ts``` file and add the following options to prevent SSR on all pages. All pages will inherit this layout.

``` js
// src/routes/+layout.ts
export const prerender = true;
export const ssr = false;
export const csr = true;
```

### Create general layout

This adds all the necessary functionality to the application. That includes theme switching and the toast system.

``` svelte
<!-- src/routes/+layout.svelte -->
<script lang="ts">
  import "../app.css";
  import { Toaster } from "test-two-ui/ui/sonner";
  import { ModeWatcher } from "mode-watcher";
  let { children } = $props();
</script>

<Toaster />
<ModeWatcher />
{@render children?.()}
```

### Create basic homepage

This basic homepage imports our default layout and gives an example of the toast system.

``` svelte
<!-- src/routes/+page.svelte -->
<script lang="ts">
  import { toast } from "svelte-sonner";
  import { Layout, Insert } from "test-two-ui/layout/general";
  import { Button } from "test-two-ui/ui/button";
  let sidebarOpen = $state<boolean>(true);
  const pageName = "Home";
</script>

<svelte:head>
  <title>{pageName}</title>
</svelte:head>

<Layout name={pageName} {sidebarOpen}>
  <Insert>
    <Button
      onclick={() => {
        toast("Hello world");
      }}>Show toast</Button
    >
  </Insert>
</Layout>
```

### Configure tailwind

This configures all the CSS needed for tailwind and shadcn to work, as well as imports the default tailwind color scheme from the library and applies it.

``` css
/* src/app.css */

@import "tailwindcss";
@import "tw-animate-css";

/* Import theme from library */
@import "test-two-ui/themes/base.css";

/* Enable theme for components in library */
@source "../node_modules/test-two-ui/**/*";

@plugin '@tailwindcss/forms';
@plugin '@tailwindcss/typography';

@custom-variant dark (&:is(.dark *));

@theme inline {
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
}

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

### Nice to have

``` sh
# Install charting types
npm i -D @types/d3
```

## Building

This project was created as a SvelteKit library that gets built using ```npm pack```.

To publish the package you simply need to update the version with npm. THis will create a new commit and tag matching the version in your ```package.json```. We have a GitHub action that will run the build when it sees a new version tag. Then it will add the build to the GitHub repo Releases.

Currently we do not publish this library to npm as this is an internal library. This git flow allows us to easy maintain the library while keeping it private.

``` sh
npm version patch
npm version minor
npm version major

git push && git push --tags
```

## Development

We have created a local storybook to preview our custom components and layouts. We only display our custom components and themes, all the default shadcn components can be viewed in their documentation.

``` sh
npm run storybook
```

## Original SvelteKit README

Everything you need to build a Svelte library, powered by [`sv`](https://npmjs.com/package/sv).

Read more about creating a library [in the docs](https://svelte.dev/docs/kit/packaging).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```sh
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```sh
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

Everything inside `src/lib` is part of your library, everything inside `src/routes` can be used as a showcase or preview app.

## Building

To build your library:

```sh
npm pack
```

To create a production version of your showcase app:

```sh
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.

## Publishing

Go into the `package.json` and give your package the desired name through the `"name"` option. Also consider adding a `"license"` field and point it to a `LICENSE` file which you can create from a template (one popular option is the [MIT license](https://opensource.org/license/mit/)).

To publish your library to [npm](https://www.npmjs.com):

```sh
npm publish
```
