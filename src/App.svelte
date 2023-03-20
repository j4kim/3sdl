<script>
  import map from "./map.js";

  let innerWidth = 0;
  let innerHeight = 0;

  $: px = innerWidth / map[0].length;
</script>

<main>
  <svg width={innerWidth} height={innerHeight}>
    {#each map as row, y}
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
    {/each}
  </svg>
</main>

<svelte:window bind:innerWidth bind:innerHeight />

<style>
  :global(body) {
    margin: 0;
  }
</style>
