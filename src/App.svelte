<script>
  import map from "./map.js";
</script>

<main>
  <svg>
    {#each map as row, y}
      {#each row as cell, x}
        <rect
          x={10 * x}
          y={10 * y}
          width="10"
          height={10}
          fill={cell === "X" ? "red" : ""}
        />
      {/each}
    {/each}
  </svg>
</main>

<style>
  :global(body) {
    margin: 0;
  }
</style>
