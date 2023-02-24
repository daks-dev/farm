<script lang="ts">
  import { BROWSER } from 'esm-env';
  import {
    lazyload,
    YandexMetrikaInit,
    RouteTransition,
    Footer,
    Navbar,
    ScreenBlock
  } from 'daks-svelte';

  import '../app.css';
  import '$iconify';

  import type { PageData } from './$types';
  export let data: PageData;

  import { app, nav } from '$configs';

  // window.matchMedia('(prefers-color-scheme: dark)').matches
  if (BROWSER) {
    if (!('color-theme' in localStorage)) {
      localStorage.setItem('color-theme', 'dark');
      document.documentElement.classList.add('dark');
    }
    document.lazyload ??= lazyload();
  }
</script>

<svelte:head>
  <meta
    name="theme-color"
    content={app.themeColor} />
  <meta
    name="msapplication-TileColor"
    content={app.tileColor} />
  <meta
    name="application-name"
    content={app.shortName} />
  <meta
    name="apple-mobile-web-app-title"
    content={app.shortName} />
</svelte:head>

<RouteTransition
  class="flex flex-col grow"
  referesh={data.referesh}
  mode="1">
  <slot />
</RouteTransition>

<Footer
  class="bg-neutral-200/50 dark:bg-inherit"
  {...nav.footer} />

<Navbar
  class="bg-neutral-50 dark:bg-inherit
         fixed:bg-neutral-50/95 dark:fixed:bg-slate-700/95
         shadow-sm dark:shadow-md fixed:shadow-lg"
  {...nav.navbar} />

<ScreenBlock
  class="bg-neutral-100 dark:bg-gray-800"
  delay={100} />

<YandexMetrikaInit />
