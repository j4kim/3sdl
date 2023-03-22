<script>
  import map from "./map.js";
  import Row from "./Row.svelte";

  let innerWidth = 100;
  let innerHeight = 100;

  let mapRows = map.length;
  let mapCols = map[0].length;

  $: px = innerWidth / mapCols;

  $: mapHeight = px * mapRows;

  $: remainingHeight = innerHeight - mapHeight;

  $: additionalRows = Math.floor(remainingHeight / px);

  $: additionalRowsUp = Math.round(additionalRows / 2);

  $: additionalRowsDown = additionalRows - additionalRowsUp;
</script>

<main>
  <svg width={innerWidth} height={innerHeight}>
    {#each map as row, y}
      <Row {row} y={y + additionalRowsUp} {px} />
    {/each}
  </svg>
</main>

<svelte:window bind:innerWidth bind:innerHeight />

<style>
  :global(body) {
    margin: 0;
  }
</style>
