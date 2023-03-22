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
</script>

<svg {width} {height} fill="rgb(31, 38, 49)">
  {#each rows as row, y}
    <Row {row} {y} {px} />
  {/each}
</svg>

<style>
  svg {
    display: block;
  }
</style>
