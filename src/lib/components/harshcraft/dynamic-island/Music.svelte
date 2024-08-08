<script>
  import { cn } from "$lib/utils";
  import { onDestroy, onMount } from "svelte";
  import { draw, fade, scale } from "svelte/transition";

  let totalTime = 2 * 60 + 21;
  let timeElapsed = 0;
  let active = true;
  let timerId;

  onDestroy(() => {
    clearInterval(timerId);
  });

  let runActive = () => {
    if (active) {
      timerId = setInterval(() => {
        timeElapsed += 1;
      }, 1000);
    } else {
      clearInterval(timerId);
    }
  };
  onMount(() => {
    runActive();
  });

  $: minutes = Math.floor(timeElapsed / 60);
  $: seconds = timeElapsed % 60;

  $: progressPercentage = (timeElapsed / totalTime) * 100;
  let allPaths = [
    "M2 10v3",
    "M6 6v11",
    "M10 3v18",
    "M14 8v7",
    "M18 5v13",
    "M22 10v3",
  ];
</script>

<div class="mx-4 flex w-full flex-col">
  <div class="flex items-center justify-between">
    <div class="flex items-center">
      <img
        src="https://i.pinimg.com/736x/9a/1f/8c/9a1f8c95da0a03746023d277dd315d5e.jpg"
        width="48"
        height="48"
        class="rounded-md"
        alt=""
      />
      <div class="ml-2 flex flex-col">
        <span class="flex items-center text-xs font-medium text-neutral-100">
          Lonestar Lucahdor
          <svg
            width="10"
            height="10"
            viewBox="0 0 36 36"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            class="ml-1"
          >
            <rect width="36" height="36" rx="6" fill="white" />
            <path
              d="M12 27V9H23.9653V12.1377H15.7543V16.4268H23.3497V18.5645H15.7543V23.8623H24V27H12Z"
              fill="black"
            />
          </svg>
        </span>
        <span class="mt-0.5 text-xs text-neutral-500"> That Mexican OT </span>
      </div>
    </div>
    <div class="flex items-center gap-x-0.5">
      {#key active}
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-audio-lines"
          ><path d={allPaths[0]} />
          <path d={allPaths[1]} />
          <path d={allPaths[2]} />
          <path d={allPaths[3]} />
          <path d={allPaths[4]} />
          <path d={allPaths[5]} />
        </svg>
      {/key}
    </div>
  </div>
  <div class="mb-4 mt-2 flex items-center justify-center gap-x-2">
    <span class="w-5 text-[10px] text-neutral-400">
      {minutes}:{seconds < 10 ? `0${seconds}` : seconds}
    </span>
    <div class="h-1 w-[232px] overflow-hidden rounded-full bg-neutral-700">
      <div
        class="h-1 rounded-full bg-neutral-50"
        style="transition: width 1s; width: {progressPercentage}%;"
      />
    </div>
    <span class="w-5 text-[10px] text-neutral-400">-2:21</span>
  </div>
  <div class="flex items-center justify-between gap-x-2">
    <button class="text-xl text-neutral-500">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="18"
        height="18"
        viewBox="0 0 24 24"
        fill="#737373"
        stroke="currentColor"
        stroke-width="1.4"
        stroke-linecap="round"
        stroke-linejoin="round"
        ><polygon
          points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"
        /></svg
      >
    </button>
    <div class="flex items-center gap-x-3">
      <button class="text-xl text-neutral-100">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="18"
          height="18"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="1.4"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-rewind"
          ><polygon points="11 18 2 12 11 5 11 18" /><polygon
            points="22 18 13 12 22 5 22 18"
          /></svg
        >
      </button>
      <button
        on:click={() => {
          active = !active;
          runActive();
        }}
        class="text-4xl text-neutral-100 outline-none"
      >
        {#if active}
          <svg
            in:scale
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="#f5f5f5"
            stroke="currentColor"
            stroke-width="1.6"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-pause"
            ><rect x="14" y="4" width="4" height="16" rx="1" /><rect
              x="6"
              y="4"
              width="4"
              height="16"
              rx="1"
            /></svg
          >
        {:else}
          <svg
            in:scale
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="#f5f5f5"
            stroke="currentColor"
            stroke-width="1.6"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-play"
            ><polygon points="6 3 20 12 6 21 6 3" /></svg
          >
        {/if}
      </button>
      <button class="text-xl text-neutral-100">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="18"
          height="18"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="1.4"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-fast-forward"
          ><polygon points="13 18 22 12 13 5 13 18" /><polygon
            points="2 18 11 12 2 5 2 18"
          /></svg
        >
      </button>
    </div>
    <button class="text-lg text-neutral-500 outline-none">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="18"
        height="18"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.4"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="lucide lucide-podcast"
        ><path d="M16.85 18.58a9 9 0 1 0-9.7 0" /><path
          d="M8 14a5 5 0 1 1 8 0"
        /><circle cx="12" cy="11" r="1" /><path
          d="M13 17a1 1 0 1 0-2 0l.5 4.5a.5.5 0 1 0 1 0Z"
        /></svg
      >
    </button>
  </div>
</div>
