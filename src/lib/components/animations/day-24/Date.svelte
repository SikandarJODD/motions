<script>
  import { ChevronRight, ChevronLeft } from "lucide-svelte";
</script>

<div >
  <div class="mb-4 grid grid-cols-3 items-center px-2">
    <button class="outline-none">
      <ChevronLeft size="24" strokeWidth={1.4} />
    </button>
    <button>August</button>
    <div class="flex justify-end">
      <button class="outline-none">
        <ChevronRight size="24" strokeWidth={1.4} />
      </button>
    </div>
  </div>
  <div class="grid grid-cols-7">
    {#each { length: 30 } as _, index}
      <button
        on:click
        class="flex aspect-square items-center justify-center rounded-md text-center hover:bg-[#EAEAEA] active:bg-[#dcdcdc]"
      >
        {index + 1}
      </button>
    {/each}
  </div>
</div>
<!-- on:click is used here for onCloseHandler which is defined in EachEvent component -->
