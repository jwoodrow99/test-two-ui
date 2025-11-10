<script module>
  import { defineMeta } from "@storybook/addon-svelte-csf";

  import { Layout, Insert } from "$lib/components/layout/general/index.js";

  // More on how to set up stories at: https://storybook.js.org/docs/writing-stories
  const { Story } = defineMeta({
    component: Layout,
    parameters: {
      layout: "none",
    },
  });
</script>

<!-- More on writing stories with args: https://storybook.js.org/docs/writing-stories/args -->
<Story name="Primary">
  <Insert>
    <h1 class="col-span-12">This is the general layout.</h1>
  </Insert>
</Story>
