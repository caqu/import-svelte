<script>
  import { fade } from "svelte/transition";
</script>

<div out:fade>
  This is content from a dynamically loaded module instantiated as a child
  component. This div has a a out:fade outro.
</div>
