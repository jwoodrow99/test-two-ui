<script lang="ts">
  import type { Component, Snippet } from "svelte";

  let { children } = $props<{
    children?: Snippet;
  }>();
</script>

<div class="grid grid-cols-12 gap-4">
  {@render children?.()}
</div>
