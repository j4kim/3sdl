<script>
  import { wide, narrow } from "./maps.js";
  import Map from "./Map.svelte";

  let clientWidth;
  let clientHeight;

  let redrawnMap;
  let rows;

  $: width = 0.98 * clientWidth;
  $: maxHeight = 0.99 * clientHeight;

  $: ratio = width / maxHeight;
  $: map =
    redrawnMap ?? (ratio > 1 ? wide : narrow).map((row) => row.split(""));

  let mouseDown = false;
  let rectId;
  let newValue;

  function toggle(x, y) {
    const rowsClone = [...rows];
    const rowClone = [...rowsClone[y]];
    if (!newValue) {
      newValue = rowClone[x] === "X" ? " " : "X";
    }
    rowClone[x] = newValue;
    rowsClone[y] = rowClone;
    redrawnMap = rowsClone;
  }

  function toggleRect(target) {
    if (target.nodeName !== "rect") return;
    rectId = target.id;
    const { x, y } = target.dataset;
    toggle(x, y);
  }

  function handleMouseDown({ target }) {
    mouseDown = true;
    toggleRect(target);
  }

  function handleMouseMove({ target }) {
    if (!mouseDown) return;
    if (rectId === target.id) return;
    toggleRect(target);
  }

  function reset() {
    mouseDown = false;
    rectId = null;
    newValue = null;
  }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<main
  bind:clientWidth
  bind:clientHeight
  on:mousedown={handleMouseDown}
  on:mousemove={handleMouseMove}
  on:mouseup={reset}
>
  {#if clientHeight}
    <Map {map} {width} {maxHeight} bind:rows />
  {/if}
</main>

<style>
  :global(body) {
    margin: 0;
    background-color: rgb(41, 102, 199);
  }
  main {
    height: 100dvh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }
</style>
