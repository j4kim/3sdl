<script>
  import map from "./map.js";
  import Row from "./Row.svelte";

  let clientWidth = 100;
  let clientHeight = 100;

  const mapRows = map.length;
  const mapCols = map[0].length;
  const defaultRow = " ".repeat(mapCols);

  $: width = 0.98 * clientWidth;
  $: maxHeight = 0.99 * clientHeight;

  $: px = +(width / mapCols).toFixed(2);

  $: mapHeight = px * mapRows;

  $: remainingHeight = maxHeight - mapHeight;

  $: additionalRows = Math.floor(remainingHeight / px);

  $: height = mapHeight + additionalRows * px;

  $: rowsBefore = Math.round(additionalRows / 2);

  $: rowsAfter = additionalRows - rowsBefore;

  $: allRows = [
    ...(rowsBefore > 0 ? Array(rowsBefore).fill(defaultRow) : []),
    ...map,
    ...(rowsAfter > 0 ? Array(rowsAfter).fill(defaultRow) : []),
  ];
</script>

<main bind:clientWidth bind:clientHeight>
  <svg {width} {height} fill="rgb(31, 38, 49)">
    {#each allRows as row, y}
      <Row {row} {y} {px} />
    {/each}
  </svg>
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
  }
  svg {
    display: block;
  }
</style>
