<script>
  import Cell from "./Cell.svelte";

  export let row;
  export let px;
  export let y;
</script>

{#each row as cell, x}
  <Cell {x} {y} {px} fill={cell === "X" ? "white" : ""} />
{/each}
