<script>
  import { getContext } from "svelte";

  let klass = "";

  export let name;

  const current = getContext("fullpage");
</script>

<section {name}>
  {#if name === $current}
    <slot />
  {/if}
</section>
