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
/>
