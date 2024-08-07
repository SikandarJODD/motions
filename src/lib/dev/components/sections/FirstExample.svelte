<script>
  import ClipPath from "$lib/components/animations/ClipPath/ClipPath.svelte";
  import Day20 from "$lib/components/animations/day-20/Day20.svelte";
  import Day31 from "$lib/components/animations/day-31/Day31.svelte";
  import Day4 from "$lib/components/animations/day-4/Day4.svelte";
  let components = [
    {
      id: 1,
      name: "Day20",
      component: Day20,
    },
    {
      id: 2,
      name: "Day4",
      component: Day4,
    },
    {
      id: 3,
      name: "Day31",
      component: Day31,
    },
    {
      id: 4,
      name: "ClipPath",
      component: ClipPath,
    },
  ];
</script>

<div class="grid grid-cols-1 gap-4 lg:grid-cols-2 lg:gap-6 mb-10">
  {#each components as { component }}
    <div
      class="min-h-96 overflow-hidden flex justify-center items-center p-4 md:p-6 rounded-2xl border"
    >
      <svelte:component this={component} />
    </div>
  {/each}
</div>
