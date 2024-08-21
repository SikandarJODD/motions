<script>
  import "./day13.css";
  import SvelteSvg from "$lib/imgs/svelte.svg";
  import SvelteTransparent from "$lib/imgs/sveltetransparent.svg";
  import { onMount } from "svelte";

  let canvas;
  let context;

  const canvasWidth = 600;
  const canvasHeight = 600;

  let rectanglesPerRow = Math.floor((canvasWidth - 10) / 10);
  let rectanglesPerColumn = Math.floor((canvasHeight - 10) / 10);
  let totalRectangles = rectanglesPerRow * rectanglesPerColumn;

  let rectangles = [];

  // Initialize rectangles array
  for (let i = 0; i < totalRectangles; i++) {
    rectangles.push({
      x: 10 + (i % rectanglesPerRow) * 10,
      y: 10 + Math.floor(i / rectanglesPerRow) * 10,
      width: 2,
      height: 2,
      opacity: 1,
      phase: Math.random() * Math.PI * 4,
    });
  }

  function draw() {
    context.clearRect(0, 0, canvasWidth, canvasHeight);

    rectangles.forEach((rect) => {
      const time = (window.performance.now() / 1000) * 2;
      rect.opacity = 0.3 + 0.3 * Math.sin(time + rect.phase);

      context.fillStyle = `rgba(255, 62, 0, ${rect.opacity})`;
      context.fillRect(rect.x, rect.y, rect.width, rect.height);
    });

    requestAnimationFrame(draw);
  }

  onMount(() => {
    context = canvas.getContext("2d");
    draw();
  });
</script>

<div class="wrapper">
  <img src={SvelteSvg} alt="svelte-real-img" class="real-image w-10 h-10 z-[1000]" />
  <img
    src={SvelteTransparent}
    alt="svelte-transparent"
    class="transparent-image w-10"
  />
  <h3 class='font-medium'>Svelte</h3>
  <div class="background"></div>
  <canvas
    bind:this={canvas}
    width={canvasWidth}
    height={canvasHeight}
    id='canvas'
  ></canvas>
</div>
