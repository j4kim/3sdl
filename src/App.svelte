<script>
  import map from "./map.js";
  import Row from "./Row.svelte";

  let innerWidth = 0;
  let innerHeight = 0;

  $: px = innerWidth / map[0].length;
</script>

<main>
  <svg width={innerWidth} height={innerHeight}>
    {#each map as row, y}
      <Row {row} {y} {px} />
    {/each}
  </svg>
</main>

<svelte:window bind:innerWidth bind:innerHeight />

<style>
  :global(body) {
    margin: 0;
  }
</style>
