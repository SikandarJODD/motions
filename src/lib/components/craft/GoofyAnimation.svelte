<script>
  import Slider from "../ui/slider/slider.svelte";

  let value = 10;
</script>

<div
  class="flex justify-center items-center gap-14 bg-white min-h-[500px] px-20"
  style="filter: blur(18px) contrast(40);"
>
  <div
    class="size-28 bg-neutral-800 rounded-full"
    style="transform: translateX({value * 4.32}px); "
  ></div>
  <div
    class="size-28 bg-neutral-800 rounded-full"
    style="transform: translateX({(value * 4.32) / 2}px); "
  ></div>
  <div class="size-28 bg-neutral-800 rounded-full"></div>
  <div
    class="size-28 bg-neutral-800 rounded-full"
    style="transform: translateX(-{(value * 4.32) / 2}px);"
  ></div>
  <div
    class="size-28 bg-neutral-800 rounded-full"
    style="transform: translateX({-value * 4.32}px);"
  ></div>
</div>
<div class="mt-20 z-[10000] w-32">
  <input
    type="range"
    min="0"
    max="78"
    bind:value
    class="border rounded-full appearance-none bg-white h-3 
    w-full outline-none cursor-pointer
    "
    style="--thumb-size: 25px;"
  />
</div>

<style>
</style>
