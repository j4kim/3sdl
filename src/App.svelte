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

  $: rowsBefore = Math.round(additionalRows / 2);

  $: rowsAfter = additionalRows - rowsBefore;
</script>

<main>
  <svg width={innerWidth} height={innerHeight}>
    {#each { length: rowsBefore } as _, y}
      <Row row={map[0]} {y} {px} />
    {/each}
    {#each map as row, y}
      <Row {row} y={y + rowsBefore} {px} />
    {/each}
    {#each { length: rowsAfter } as _, y}
      <Row row={map[0]} y={rowsBefore + mapRows + y} {px} />
    {/each}
  </svg>
</main>

<svelte:window bind:innerWidth bind:innerHeight />

<style>
  :global(body) {
    margin: 0;
  }
  svg {
    display: block;
  }
</style>
