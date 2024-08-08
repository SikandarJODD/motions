<script>
  import { onMount } from "svelte";
  import { spring } from "svelte/motion";
  import FaceId from "./FaceId.svelte";
  import { fade } from "svelte/transition";
  import CallingComp from "./CallingComp.svelte";
  import Music from "./Music.svelte";

  let state = 0;
  let width = spring(96, { stiffness: 0.2, damping: 1.2 });
  let height = spring(96, { stiffness: 0.2, damping: 1.2 });
  let radius = spring(28, { stiffness: 0.2, damping: 1.2 });
  let buttons = [
    {
      label: "Idle",
      dimensions: {
        w: 100,
        h: 28,
        r: 28,
      },
    },
    {
      label: "Face ID",
      dimensions: { w: 96, h: 96, r: 28 },
    },
    {
      label: "Call",
      dimensions: { w: 284, h: 56, r: 99 },
    },
    {
      label: "Music",
      dimensions: { w: 324, h: 144, r: 32 },
    },
  ];
  onMount(() => {
    width.set(buttons[state].dimensions.w);
    height.set(buttons[state].dimensions.h);
    radius.set(buttons[state].dimensions.r);
  });
</script>

<div
  style="
    width: {$width}px;
    height: {$height}px;
    border-radius: {$radius}px;
    "
  class="absolute top-0 mb-36 mt-6 flex select-none items-center justify-center overflow-hidden bg-black"
>
  {#if state === 1}
    <div in:fade>
      <FaceId />
    </div>
  {:else if state === 2}
    <CallingComp />
  {:else if state === 3}
    <Music />
  {/if}
</div>

<div
  class="absolute bottom-4 w-fit px-6 flex items-center justify-center gap-x-2 border-t border-t-neutral-200 bg-neutral-100 py-3 dark:border-t-neutral-700/50 dark:bg-neutral-800 rounded-xl shadow-md"
>
  {#each buttons as item, index}
    <button
      class="rounded border border-neutral-400/50 bg-neutral-50 px-3 py-1 text-sm dark:border-neutral-600 dark:bg-neutral-700"
      on:click={() => {
        state = index;
        width.set(item.dimensions.w);
        height.set(item.dimensions.h);
        radius.set(item.dimensions.r);
      }}
    >
      {item.label}
    </button>
  {/each}
</div>
