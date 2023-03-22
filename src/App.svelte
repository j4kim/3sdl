<script>
  import { wide, narrow } from "./maps.js";
  import Map from "./Map.svelte";

  let clientWidth;
  let clientHeight;

  $: width = 0.98 * clientWidth;
  $: maxHeight = 0.99 * clientHeight;

  $: ratio = width / maxHeight;
  $: map = ratio > 1 ? wide : narrow;
</script>

<main bind:clientWidth bind:clientHeight>
  {#if clientHeight}
    <Map {map} {width} {maxHeight} />
  {/if}
</main>

<style>
  :global(body) {
    margin: 0;
    background-color: rgb(31, 38, 49);
  }
  main {
    height: 100dvh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }
</style>
