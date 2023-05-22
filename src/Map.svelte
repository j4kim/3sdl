<script>
  import Row from "./Row.svelte";

  export let map;
  export let width;
  export let maxHeight;

  $: mapRows = map.length;
  $: mapCols = map[0].length;
  $: defaultRow = " ".repeat(mapCols).split("");

  $: px = +(width / mapCols).toFixed(2);

  $: mapHeight = px * mapRows;

  $: remainingHeight = maxHeight - mapHeight;

  $: additionalRows = Math.floor(remainingHeight / px);

  $: height = Math.max(mapHeight + additionalRows * px, mapHeight);

  $: rowsBefore = Math.round(additionalRows / 2);

  $: rowsAfter = additionalRows - rowsBefore;

  export let rows;

  $: rows = [
    ...(rowsBefore > 0 ? Array(rowsBefore).fill(defaultRow) : []),
    ...map,
    ...(rowsAfter > 0 ? Array(rowsAfter).fill(defaultRow) : []),
  ];

  function save() {
    localStorage.saved = JSON.stringify(rows);
  }
</script>

<svg
  {width}
  {height}
  fill="rgb(31, 38, 49)"
  style="--cols:{mapCols}; --rows:{mapRows}"
>
  {#each rows as row, y}
    <Row {row} {y} {px} />
  {/each}
  <text y={height} dx="10" dy="-10" on:click={save} on:keydown={save}>📸</text>
</svg>

<style>
  svg {
    display: block;
  }
  text {
    cursor: pointer;
  }
</style>
