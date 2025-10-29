<script module>
  import { defineMeta } from "@storybook/addon-svelte-csf";
  import { Button } from "$lib/components/ui/button/index.js";

  // More on how to set up stories at: https://storybook.js.org/docs/writing-stories
  const { Story } = defineMeta({
    component: Button,
  });
</script>

<!-- More on writing stories with args: https://storybook.js.org/docs/writing-stories/args -->
<Story name="Primary">Click Me</Story>
