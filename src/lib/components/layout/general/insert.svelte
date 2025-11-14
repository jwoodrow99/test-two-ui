<script lang="ts">
  import type { Component } from "svelte";

  let { children } = $props<{
    children?: Component<any>;
  }>();
</script>

<div class="grid grid-cols-12 gap-4">
  {@render children?.()}
</div>
