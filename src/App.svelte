<script>
  import map from "./map.js";
</script>

<main>
  {#each map as row}
    <pre>{row}</pre>
  {/each}
</main>

<style>
  :global(body) {
    margin: 0;
  }
</style>
