<script>
  import { onMount, setContext } from "svelte";
  import { writable } from "svelte/store";

  import NavIcon from "$lib/elements/NavIcon.svelte";

  export let wrap = false;
  export let wheels = false;
  export let noArrows = false;
  export let noClick = false;
  export let noDrag = false;

  let main;
  let sections = [];
  let sectionsCount = 0;

  let current = writable("");
  setContext("fullpage", current);

  let currentIndex = 0;
  $: $current = sections[currentIndex];

  onMount(() => {
    sectionsCount = main.childElementCount;
    sections = Array.from(main.children).map((e) => e.attributes.name.value);
    $current = sections[currentIndex];
  });

  function moveDown() {
    if (!wrap && currentIndex === sectionsCount - 1) return;

    currentIndex = (currentIndex + 1) % sectionsCount;
  }

  function moveUp() {
    if (!wrap && currentIndex === 0) return;

    currentIndex = (sectionsCount + currentIndex - 1) % sectionsCount;
  }

  function handleClick(_event) {
    if (noClick) return;

    moveDown();
  }

  function handleKeydown(event) {
    if (noArrows) return;

    switch (event.key) {
      case "ArrowDown":
        moveDown();
        break;
      case "ArrowUp":
        moveUp();
        break;
      default:
        break;
    }
  }

  function handleMouseWheel(event) {
    if (!wheels) return;

    if (event.wheelDeltaY < 0) moveDown();
    if (event.wheelDeltaY > 0) moveUp();
  }

  function handleDrag(event) {
    console.log(event);
  }

  let touchPosition = undefined;

  function handleTouch(event) {
    if (noDrag) return;

    if (!touchPosition) {
      touchPosition = event.changedTouches[0].pageY;
      return;
    }

    if (touchPosition > event.changedTouches[0].pageY) {
      moveDown();
    } else {
      moveUp();
    }

    touchPosition = undefined;
  }
</script>

<svelte:window
  on:keydown={handleKeydown}
  on:mousewheel={handleMouseWheel}
  on:drag={handleDrag}
  on:touchstart={handleTouch}
  on:touchend={handleTouch}
/>

<div id="fullpage" on:click={handleClick}>
  <nav>
    {#each sections as section, index}
      <NavIcon
        on:navigate={() => (currentIndex = index)}
        active={$current === section}
      />
    {/each}
  </nav>
  <main bind:this={main}>
    <slot />
  </main>
</div>

<style>
  #fullpage {
    position: relative;
    padding: 0;
    margin: 0;
    width: 100vw;
    height: 100vh;
  }

  nav {
    position: absolute;
    right: 1rem;
  }
</style>
