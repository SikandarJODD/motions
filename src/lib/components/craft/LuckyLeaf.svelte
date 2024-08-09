<script>
    import { onMount } from "svelte";
    import { draw, fade, fly } from "svelte/transition";
  
    let allPaths = [
      "M16.17 7.83 2 22",
      "M4.02 12a2.827 2.827 0 1 1 3.81-4.17A2.827 2.827 0 1 1 12 4.02a2.827 2.827 0 1 1 4.17 3.81A2.827 2.827 0 1 1 19.98 12a2.827 2.827 0 1 1-3.81 4.17A2.827 2.827 0 1 1 12 19.98a2.827 2.827 0 1 1-4.17-3.81A1 1 0 1 1 4 12",
      "m7.83 7.83 8.34 8.34",
    ];
    let mount = false;
    onMount(() => {
      mount = true;
    });
    let text = ["Luckiest", "&", "Prettiest"];
  </script>
  
  <div class=" relative flex justify-center items-center min-h-[80vh] flex-col">
    {#if mount}
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="36"
        height="36"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.6"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="lucide lucide-clover"
        ><path in:draw={{ duration: 700 }} d={allPaths[0]} />
        <path in:draw={{ duration: 2400 }} d={allPaths[1]} />
        <path in:draw={{ duration: 600, delay: 200 }} d={allPaths[2]} />
      </svg>
    {/if}
    <div class="w-full mx-auto flex justify-center items-center mt-4 gap-1.5">
      {#if mount}
        <p in:fly={{ y: 20, delay: 1500 }}>{text[0]}</p>
        <p in:fly={{ y: 20, delay: 1800 }}>{text[1]}</p>
        <p in:fly={{ y: 20, delay: 2000 }}>{text[2]}</p>
      {/if}
    </div>
  </div>
  