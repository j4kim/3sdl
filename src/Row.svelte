<script>
  export let row;
  export let px;
  export let y;
</script>

<g>
  {#each row as cell, x}
    <rect
      x={px * x}
      y={px * y}
      width={px}
      height={px}
      fill={cell === "X" ? "white" : ""}
    />
  {/each}
</g>
