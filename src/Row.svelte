<script>
  export let row;
  export let px;
  export let y;
</script>

{#each row as cell, x}
  <rect
    data-x={x}
    data-y={y}
    x={px * x}
    y={px * y}
    width={px}
    height={px}
    fill={cell === "X" ? "white" : ""}
  />
{/each}
