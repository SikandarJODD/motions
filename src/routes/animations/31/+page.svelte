<script>
  import { flip } from "svelte/animate";
  import { cubicOut } from "svelte/easing";
  import { crossfade, fade, scale } from "svelte/transition";
  const [send, receive] = crossfade({
    duration: 200,
  });
  let active = true;

  const buttons = ["dimensions", "aspect-ratio", "prompt"];
  let index = "prompt";
</script>

<div
  class=" overflow-hidden flex justify-center items-center w-full min-h-screen relative"
>
  {#if active}
    <button
      in:receive={{ key: "wrap", easing: cubicOut }}
      out:send={{ key: "wrap", easing: cubicOut }}
      class="absolute group flex h-12 w-32 items-center justify-center gap-1 border border-border bg-[#161716] p-2 active:bg-[#222422] rounded-xl"
      on:click={() => {
        active = !active;
      }}
    >
      <span
        class="inline-block text-[#929292] group-hover:text-white"
        in:receive={{ key: "text" }}
        out:send={{ key: "text" }}
      >
        Add Style
      </span>
      <span>
        <svg
          in:receive={{ key: "action", duration: 600 }}
          xmlns="http://www.w3.org/2000/svg"
          width="18"
          height="18"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="1.7"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-plus"
          ><path d="M5 12h14" /><path d="M12 5v14" /></svg
        >
      </span>
    </button>
  {:else}
    <div
      in:receive={{ key: "wrap" }}
      out:send={{ key: "wrap" }}
      class="absolute w-full max-w-96 overflow-hidden border border-border bg-[#161716] p-2 rounded-xl"
    >
      <span
        class="sr-only pointer-events-none inline-block opacity-0"
        in:receive={{ key: "text" }}
        out:send={{ key: "text" }}
      >
        Add Style
      </span>
      <header class="flex items-center justify-between">
        <div class="flex justify-center gap-2">
          {#each buttons as button}
            <button
              class="relative h-7 text-sm capitalize {button === index
                ? 'text-white'
                : 'text-[#929292]'} px-2"
              on:click={async () => {
                await new Promise((r) => setTimeout(r, 100));
                index = button;
              }}
            >
              <span class="relative z-10">
                {button.replaceAll("-", " ")}
              </span>
              <div
                class="absolute pointer-events-auto inset-0 rounded bg-[#1D1E1D]"
                style="transform-origin: 0px;"
              ></div>
            </button>
          {/each}
        </div>
        <button
          on:click={() => {
            active = true;
          }}
          class="text-2xl text-[#929292] rotate-45"
        >
          <svg
            out:send={{ key: "action",duration: 600 }}
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="1.7"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-plus"
            ><path d="M5 12h14" /><path d="M12 5v14" /></svg
          >
        </button>
      </header>
      <div>
        {#if index === "dimensions"}
          <div>
            <div class="flex h-24 items-center justify-center">Dimensions</div>
            <div class="flex justify-between pl-2">
              <small class="flex items-center gap-2 text-[#929292]">
                <div class="h-1 w-1 rounded-full bg-[#FDFF79]"></div>
                Changes
              </small>
              <button class="h-8 rounded-md bg-[#FDFF79] px-2 text-black">
                Apply changes
              </button>
            </div>
          </div>
        {:else if index === "aspect-ratio"}
          <div>
            <div class="flex h-20 items-center justify-center">
              Aspect ratio
            </div>
            <div class="flex justify-between pl-2">
              <small class="flex items-center gap-2 text-[#929292]">
                <div class="h-1 w-1 rounded-full bg-[#FDFF79]"></div>
                Changes
              </small>
              <button class="h-8 rounded-md bg-[#FDFF79] px-2 text-black">
                Apply changes
              </button>
            </div>
          </div>
        {:else if index === "prompt"}
          <div>
            <div class="flex h-32 items-center justify-center">Prompt</div>
            <div class="flex justify-between pl-2">
              <small class="flex items-center gap-2 text-[#929292]">
                <div class="h-1 w-1 rounded-full bg-[#FDFF79]"></div>
                Changes
              </small>
              <button class="h-8 rounded-md bg-[#FDFF79] px-2 text-black">
                Apply changes
              </button>
            </div>
          </div>
        {/if}
      </div>
    </div>
  {/if}
</div>
