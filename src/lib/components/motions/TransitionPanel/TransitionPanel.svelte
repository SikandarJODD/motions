<script>
  import Button from "$lib/components/ui/button/button.svelte";
  import { cubicOut, sineOut } from "svelte/easing";
  import { fly } from "svelte/transition";

  let features = [
    {
      title: "Brand",
      description:
        "Develop a distinctive brand identity with tailored logos and guidelines to ensure consistent messaging across all platforms.",
    },
    {
      title: "Product",
      description:
        "Create impactful websites that combine beautiful aesthetics with functional design, ensuring a superior online presence.",
    },
    {
      title: "Website",
      description:
        "Create impactful websites that combine beautiful aesthetics with functional design, ensuring a superior online presence.",
    },
    {
      title: "Design System",
      description:
        "Develop a design system that unifies your brand identity, ensuring consistency across all platforms and products.",
    },
  ];
  let state = 0;
  $: direction = false;
  $: xvalue = direction ? 24 : -24;
</script>

<div
  class="w-[364px] overflow-hidden rounded-xl border border-zinc-950/10 dark:border-zinc-100/10 shadow-sm bg-zinc-50 dark:bg-zinc-900"
>
  {#key state}
    <div in:fly={{ x: xvalue }} class="px-4 pt-4">
      <h3 class="mb-0.5 font-semibold text-lg text-zinc-800 dark:text-zinc-100 ">
        {features[state].title}
      </h3>
      <p class="text-zinc-600 dark:text-muted-foreground">
        {features[state].description}
      </p>
    </div>
  {/key}
  <div>
    <div class="flex justify-between px-4 py-2 mt-2">
      <Button
        size="sm"
        variant="secondary"
        on:click={() => {
          direction = false;
          state = state === 0 ? features.length - 1 : state - 1;
        }}>Previous</Button
      >
      <Button
        size="sm"
        variant="secondary"
        on:click={() => {
          direction = true;
          state = state === features.length - 1 ? 0 : state + 1;
        }}>Next</Button
      >
    </div>
  </div>
</div>
