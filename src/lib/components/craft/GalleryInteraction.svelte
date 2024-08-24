<script lang="ts">
  import { cn } from "$lib/utils";
  import { flip } from "svelte/animate";
  import { crossfade, fade } from "svelte/transition";
  import Button from "../ui/button/button.svelte";
  import { quintOut } from "svelte/easing";
  const [send, receive] = crossfade({
    fallback(node, params) {
      const style = getComputedStyle(node);
      const transform = style.transform === "none" ? "" : style.transform;

      return {
        duration: 600,
        easing: quintOut,
        css: (t) => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`,
      };
    },
  });

  let images = [
    {
      img: "https://i.pinimg.com/564x/17/1c/a2/171ca25053719bcd076a12e1e9d8a846.jpg",
      id: 1,
      title: "sunflowers",
    },
    {
      img: "https://i.pinimg.com/736x/2b/9a/c9/2b9ac9774f32f0cd751b1fe662e6e41c.jpg",
      id: 2,
      title: "farm",
    },
    {
      img: "https://i.pinimg.com/736x/9a/01/9c/9a019c6e20efbe52d5e838eaecd85b71.jpg",
      id: 3,
      title: "farm_land",
    },

    {
      img: "https://i.pinimg.com/564x/4e/09/0a/4e090a0d94f4b453076a186413adfbae.jpg",
      id: 6,
      title: "train",
    },
    {
      img: "https://i.pinimg.com/564x/45/ce/3b/45ce3b42da8733ad8ff8e5aa4f941913.jpg",
      id: 7,
      title: "leaf",
    },
  ];
  let selectedImg = false;
  let imgobj: {
    img: string;
    id: number;
    title: string;
  };
  let visible = true;
</script>

<div>
  <Button
    on:click={() => {
      visible = !visible;
    }}
  >
    {visible ? "Show Gallery" : "Hide Gallery"}
  </Button>
</div>
<div class="flex justify-center items-center min-h-[100vh] bg-white">
  {#if visible}
    <div
      class="w-[60%] absolute grid gap-2 {visible
        ? 'sm:grid-cols-2 md:grid-cols-9'
        : 'md:grid-cols-4'}"
    >
      {#each images as item, i (item)}
        <div
          in:receive={{ key: item }}
          out:send={{ key: item }}
          animate:flip
          class={cn(
            "h-44  rounded-lg flex items-center justify-center text-xl bg-neutral-800 w-full",
            i == 0 && "md:col-span-5",
            i == 1 && "md:col-span-4",
            i > 1 && "md:col-span-3",
            item.title
          )}
        >
          {item.id}
        </div>
      {/each}
    </div>
  {:else}
    <div
      class="w-[60%] absolute grid gap-2 {visible
        ? 'sm:grid-cols-2 md:grid-cols-9'
        : 'md:grid-cols-4'}"
    >
      {#each images as item, i (item)}
        <div
          class={cn(
            "h-56  rounded-lg flex items-center justify-center text-xl bg-neutral-800 w-full",
            i == 0 && "md:col-start-1",
            i == 1 && "md:col-span-2",
            i == 2 && "md:col-start-4",
            i > 2 && "md:col-span-2"
          )}
          in:receive={{ key: item }}
          out:send={{ key: item }}
          animate:flip
        >
          {item.id}
        </div>
      {/each}
    </div>
  {/if}
</div>
