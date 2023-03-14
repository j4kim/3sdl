<script>
  import map from "./map.js";
</script>

<main>
  {#each map as row}
    <pre>{row}</pre>
  {/each}
</main>

<style>
  main {
    font-size: 5vmin;
  }
  pre {
    margin: 0;
  }
</style>
