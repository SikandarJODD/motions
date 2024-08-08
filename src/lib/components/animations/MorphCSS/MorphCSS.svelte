<script>
  import { cn } from "$lib/utils";
  import { onMount } from "svelte";
  import { Motion } from "svelte-motion";
  let getRandomHeight = () => Math.floor(Math.random() * 120) + 60;
  let heights = [80, 80, 80, 80];
  let done = false;
  onMount(() => {
    let interval = setInterval(() => {
      if (!done) {
        heights = heights.map((h) => getRandomHeight());
      } else {
        heights = [200, 200, 200, 200];
      }
    }, 200);
    return () => clearInterval(interval);
  });
  onMount(() => {
    setTimeout(() => {
      done = true;
    }, 3000);
  });
</script>

<div
  class="relative flex h-dvh w-full flex-col items-center justify-center bg-white text-black"
>
  <div
    style="
  filter: {done ? `blur(20px) contrast(20)` : ''};
  transition : filter 0.4s;
  "
    class="flex h-full w-full items-center justify-center gap-1 bg-white"
  >
    {#each { length: 4 } as _, index}
      <Motion
        animate={{
          height: heights[index],
          width: done ? 200 : 80,
        }}
        let:motion
      >
        <div
          use:motion
          style="transition: height 0.2s, width 0.2s;
          translate: {done && index === 0
            ? '300px'
            : done && index === 1
              ? '150px'
              : done && index === 2
                ? '-100px'
                : done && index === 3
                  ? '-280px'
                  : ''} 0px;
          "
          class={cn("bg-black rounded-[999px]")}
        >
          {index}
        </div>
      </Motion>
    {/each}
  </div>
</div>
