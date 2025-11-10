<script lang="ts">
  // Ui
  import { SidebarTrigger } from "$lib/components/ui/sidebar/index.js";
  import { Separator } from "$lib/components/ui/separator/index.js";

  let {
    children,
    pageActions,
    name,
    sidebarOpen = $bindable<boolean>(),
  } = $props<{
    children?: any;
    pageActions?: any;
    name: string;
    sidebarOpen: boolean;
  }>();
</script>

<div
  class="flex flex-col transition-all w-full bg-sidebar {sidebarOpen
    ? 'md:p-4'
    : ''}"
>
  <div
    class="flex-1 transition-all bg-background {sidebarOpen
      ? 'md:rounded-xl'
      : ''}"
  >
    <div class="p-4">
      <div class="flex h-5 items-center space-x-4">
        <SidebarTrigger />
        <Separator orientation="vertical" />
        <div class="whitespace-nowrap">{name}</div>
        <div class="w-full flex justify-end h-5 items-center space-x-2 text-sm">
          {#if pageActions}
            <Separator orientation="vertical" />
            {@render pageActions?.()}
          {/if}
        </div>
      </div>
    </div>

    <Separator />

    <div class="p-4">
      {@render children?.()}
    </div>
  </div>
</div>
