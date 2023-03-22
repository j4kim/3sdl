<script>
  export let row;
  export let px;
  export let y;
</script>

{#each row as cell, x}
  <rect
    data-x={x}
    data-y={y}
    x={(px * x).toFixed(2)}
    y={(px * y).toFixed(2)}
    width={px.toFixed(2)}
    height={px.toFixed(2)}
    fill={cell === "X" ? "white" : ""}
  />
{/each}
