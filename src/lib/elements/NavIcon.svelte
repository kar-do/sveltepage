<script>
  import { slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";
  import { createEventDispatcher } from "svelte";

  export let active = false;

  const dispatcher = createEventDispatcher();
</script>

<svg
  viewbox="0 0 20 20"
  width="1rem"
  height="1rem"
  xmlns="http://www.w3.org/2000/svg"
  on:click|stopPropagation={(e) => dispatcher("navigate")}
>
  <circle cx="10" cy="10" r="5" />
  {#if active}
    <circle
      cx="10"
      cy="10"
      r="8"
      fill-opacity="0"
      stroke="black"
      stroke-width="2"
      transition:slide={{ delay: 250, duration: 300, easing: quintOut }}
    />
  {/if}
</svg>

<style>
  svg {
    display: block;
    cursor: pointer;
  }
</style>
