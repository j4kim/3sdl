<script>
  import map from "./map.js";
  import Row from "./Row.svelte";

  let innerWidth = 100;
  let innerHeight = 100;

  let mapRows = map.length;
  let mapCols = map[0].length;

  $: width = 0.98 * innerWidth;
  $: maxHeight = 0.99 * innerHeight;

  $: px = width / mapCols;

  $: mapHeight = px * mapRows;

  $: remainingHeight = maxHeight - mapHeight;

  $: additionalRows = Math.floor(remainingHeight / px);

  $: height = mapHeight + additionalRows * px;

  $: rowsBefore = Math.round(additionalRows / 2);

  $: rowsAfter = additionalRows - rowsBefore;
</script>

<main>
  <svg {width} {height}>
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
  main {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  svg {
    display: block;
  }
</style>
