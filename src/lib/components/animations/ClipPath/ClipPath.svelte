<script lang="ts">
    import {
      Motion,
      useMotionTemplate,
      useMotionValue,
      useSpring,
      useTransform,
    } from "svelte-motion";
    let yValue = useMotionValue(191 / 1.66);
    let containerRef: HTMLElement = null;
    let onMouseOver = (event: MouseEvent) => {
      if (containerRef) {
        let { top } = containerRef.getBoundingClientRect();
        yValue.set(event.clientY - top);
      }
    };
    let onMouseLeave = () => {
      yValue.set(191 / 1.66);
    };
    let yTransform = useTransform(yValue, [0, 191], [0, 100]);
    let springYValue = useSpring(yTransform, {
      stiffness: 400,
      damping: 40,
      bounce: 0,
    });
    let motionClipPath = useMotionTemplate`inset(${springYValue}% 0 0 0)`;
  
    let top = useMotionTemplate`${springYValue}%`;
  
    console.log(yValue.get());
  </script>
  
  <div>
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div
      bind:this={containerRef}
      class="relative flex h-48 w-[500px] flex-col items-center justify-center p-8"
      on:mousemove={onMouseOver}
      on:mouseleave={onMouseLeave}
    >
      <h1 class="w-full text-start text-3xl font-bold tracking-tighter">
        Svelte is <br /> Awesome dude!
      </h1>
      <!-- H1  -->
      <Motion
        style={{
          clipPath: motionClipPath,
        }}
        let:motion
      >
        <h1
          style="-webkit-text-stroke:1px #245595"
          class="absolute inset-0 flex w-full items-center bg-background p-8 text-start text-3xl font-bold tracking-tighter text-transparent"
          use:motion
        >
          Svelte is <br /> Awesome dude!
          <Motion let:motion>
            <div
              style="top:0; left:0"
              class="absolute -z-10 h-full w-full bg-gradient-to-b from-[#00346E] to-transparent"
              use:motion
            ></div>
          </Motion>
        </h1>
      </Motion>
  
      <!-- DIV -->
      <Motion style={{ top }} let:motion>
        <div
          class="absolute h-0.5 w-full rounded-full bg-[#0883E6]"
          use:motion
        ></div>
      </Motion>
  
      <!-- Svgs -->
      <div class="text-[#4C84B5]">
        <svg
          viewBox="0 0 101 99"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="absolute right-0 top-0 w-6"
        >
          <path
            d="M0.455811 3.72412H97.0376V98.9359"
            stroke="currentColor"
            stroke-width="6"
          />
        </svg>
        <svg
          viewBox="0 0 101 99"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="absolute left-0 top-0 w-6 -rotate-90"
        >
          <path
            d="M0.455811 3.72412H97.0376V98.9359"
            stroke="currentColor"
            stroke-width="6"
          />
        </svg>
        <svg
          viewBox="0 0 101 99"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="absolute bottom-0 left-0 w-6 -rotate-180"
        >
          <path
            d="M0.455811 3.72412H97.0376V98.9359"
            stroke="currentColor"
            stroke-width="6"
          />
        </svg>
        <svg
          viewBox="0 0 101 99"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="absolute bottom-0 right-0 w-6 rotate-90"
        >
          <path
            d="M0.455811 3.72412H97.0376V98.9359"
            stroke="currentColor"
            stroke-width="6"
          />
        </svg>
      </div>
    </div>
  </div>
  