<script>
  import { MessageCircleMore, Mic, Share2 } from "lucide-svelte";
  import { spring } from "svelte/motion";
  import MessageBox from "./MessageBox.svelte";
  let height = spring(54, { stiffness: 0.2, damping: 1.2 });
  let width = spring(195, { stiffness: 0.2, damping: 1.2 });
  let state = 0;
  let dimensions = [
    {
      height: 54,
      width: 195,
    },
    {
      height: 330,
      width: 220,
    },
  ];
</script>

<div
  class="relative w-full h-full flex justify-center items-center md:w-[550px] md:h-96 bg-background rounded-xl border shadow-lg"
>
  <div
    style="height: {$height}px; width:{$width}px;"
    class="absolute bottom-4 border p-2.5 rounded-lg flex items-end justify-center flex-col"
  >
    <div>
      cook
    </div>
    <div class="flex justify-center items-center gap-2">
      <button
        class="p-1.5 rounded-full bg-zing-800 hover:bg-zinc-800/70 transition-all duration-150 outline-none"
        on:click={() => {
          state = state === 0 ? 1 : 0;
          height.set(dimensions[state].height);
          width.set(dimensions[state].width);
        }}
      >
        <MessageCircleMore class="w-[18px] h-[18px] text-neutral-400" />
      </button>
      <button
        class="p-1.5 rounded-full bg-zing-800 hover:bg-zinc-800/70 transition-all duration-150"
      >
        <Mic class="w-[18px] h-[18px] text-neutral-400" />
      </button>
      <button
        class="p-1.5 rounded-full bg-zing-800 hover:bg-zinc-800/70 transition-all duration-150"
      >
        <Share2 class="w-[18px] h-[18px] text-neutral-400" />
      </button>
      <button class="border rounded-md px-2 py-1 text-xs"> Leave </button>
    </div>
  </div>
</div>
