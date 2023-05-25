<script>
  import { onMount } from "svelte";

  let canvasElement;

  onMount(() => {
    const ctx = canvasElement.getContext("2d");
    ctx.scale(10, 10);

    ctx.fillStyle = "red";
    for (let i = 0; i < 10; i += 2) {
      ctx.fillRect(0, i, 1, 1);
    }

    ctx.fillStyle = "black";
    ctx.font = '8px "Press Start 2P"';

    ctx.fillText("3sdl", 1, 9);

    console.log(ctx.getImageData(0, 0, 1, 1));
  });
</script>

<canvas
  style:background-color="white"
  width="360"
  height="90"
  bind:this={canvasElement}
/>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");
</style>
