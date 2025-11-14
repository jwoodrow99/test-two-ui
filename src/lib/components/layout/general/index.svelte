<script lang="ts">
  import type { Component, Snippet } from "svelte";

  // Ui
  import * as Sidebar from "$lib/components/ui/sidebar/index.js";

  // components
  import Page from "$lib/components/layout/general/page.svelte";

  let {
    children,
    appSidebar,
    pageSidebar,
    pageActions,
    name,
    sidebarOpen = $bindable<boolean>(true),
  } = $props<{
    children?: any;
    appSidebar?: Snippet;
    pageSidebar?: Snippet;
    pageActions?: any;
    name: string;
    sidebarOpen: boolean;
  }>();
</script>

<Sidebar.Provider bind:open={sidebarOpen}>
  <Sidebar.Root class="bg-sidebar border-sidebar p-4">
    <Sidebar.Header>
      <h1>Prism</h1>
      <h2>{name}</h2>
    </Sidebar.Header>
    <Sidebar.Content>
      {@render appSidebar?.()}
      {@render pageSidebar?.()}
    </Sidebar.Content>
    <Sidebar.Footer />
  </Sidebar.Root>
  <Page {name} {pageActions} bind:sidebarOpen>
    {@render children?.()}
  </Page>
</Sidebar.Provider>
