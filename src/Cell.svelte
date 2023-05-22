<script>
  export let px;
  export let x;
  export let y;
  export let fill;
</script>

<rect
  id="rect-{x}-{y}"
  data-x={x}
  data-y={y}
  x={(px * x).toFixed(2)}
  y={(px * y).toFixed(2)}
  width={px}
  height={px}
  {fill}
  style="--x: {x}; --y: {y};"
/>

<style>
  @keyframes entrance {
    from {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  rect {
    animation-delay: calc(var(--x) * 0.01s);
    animation-duration: calc(var(--y) * 0.1s);
    animation-name: entrance;
    animation-fill-mode: both;
  }
</style>
