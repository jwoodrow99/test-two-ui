<script lang="ts">
  let { children } = $props<{
    children?: any;
  }>();
</script>

<div class="grid grid-cols-12 gap-4">
  {@render children?.()}
</div>
