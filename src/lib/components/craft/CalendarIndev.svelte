<script lang="ts">
  import { fade, fly, scale, crossfade } from "svelte/transition";

  const [send, receive] = crossfade({
    duration: 200,
    fallback: fade,
  });
  type Calendar = {
    id: number;
    disable: boolean;
    color?: string;
    text?: string;
    img?: string;
    desc?: string;
  };
  let calendar: Calendar[] = [
    {
      id: 1,
      disable: true,
    },
    {
      id: 2,
      disable: true,
    },
    {
      id: 3,
      disable: true,
    },
    {
      id: 4,
      disable: true,
    },
    {
      id: 5,
      disable: false,
    },
    {
      id: 6,
      disable: false,
    },
    {
      id: 7,
      disable: false,
    },
    {
      id: 8,
      disable: false,
      color: "#FF4FBE",
      text: "Work",
      img: "https://i.pinimg.com/736x/48/8d/40/488d40b821f6575e42297a0bf41a5fdc.jpg",
      desc: "Work is the most important thing in life. It is the only thing that will bring you success and happiness.",
    },
    {
      id: 9,
      disable: false,
    },
    {
      id: 10,
      disable: false,
    },
    {
      id: 11,
      disable: false,
    },
    {
      id: 12,
      disable: false,
    },
    {
      id: 13,
      disable: false,
    },
    {
      id: 14,
      disable: false,
    },
    {
      id: 15,
      disable: false,
    },
    {
      id: 16,
      disable: false,
    },
    {
      id: 17,
      disable: false,
    },
    {
      id: 18,
      disable: false,
    },
    {
      id: 19,
      disable: false,
    },
    {
      id: 20,
      disable: false,
      color: "#0D7AFF",
      text: "Templates",
      img: "https://i.pinimg.com/564x/da/c8/ba/dac8ba54001c6bc0d0e6dbd320db9f2d.jpg",
      desc: "Work on Starup & Portfolio Template using Svelte Magic UI, Free feel to use it for your project.",
    },
    {
      id: 21,
      disable: false,
    },
    {
      id: 22,
      disable: false,
    },
    {
      id: 23,
      disable: false,
    },
    {
      id: 24,
      disable: false,
    },
    {
      id: 25,
      disable: false,
    },
    {
      id: 26,
      disable: false,
    },
    {
      id: 27,
      disable: false,
    },
    {
      id: 28,
      disable: false,
    },
    {
      id: 29,
      disable: false,
    },
    {
      id: 30,
      disable: false,
      color: "#FF42F9",
      text: "Svelte Magic UI",
      img: "https://i.pinimg.com/564x/1d/16/81/1d168126922129555a3d3effbf46a999.jpg",
      desc: "Svelte Magic UI is a collection of components that are built using Svelte and Tailwind CSS.",
    },
    {
      id: 31,
      disable: false,
    },
    {
      id: 32,
      disable: false,
    },
    {
      id: 33,
      disable: false,
    },
    {
      id: 34,
      disable: false,
    },
    {
      id: 35,
      disable: false,
    },
  ];
  let i = 0;
  let isHoverId = -1;
  let isOpen = -1;
</script>

<div class="">
  <div class="border border-zinc-900 bg-zinc-900 shadow-md rounded-2xl p-4">
    <h3 class="text-lg font-semibold text-gray-400">August 2024</h3>
    <div class="grid grid-cols-7 gap-[7px] mt-3 relative">
      {#each calendar as item, index}
        {#if isOpen !== index}
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <!-- svelte-ignore a11y-click-events-have-key-events -->
          <div
            in:receive|global={{ key: item.id, duration: 300 }}
            out:send|global={{ key: item.id, duration: 300 }}
            style="background-color: {item.color};"
            class="calendar-item relative w-10 h-10 rounded-lg {item.disable
              ? 'bg-zinc-700/40'
              : 'bg-zinc-600/80'} group flex justify-center items-center cursor-pointer "
            class:disabled={item.disable}
            on:click={() => {
              if (item.color) {
                isOpen = index;
              } else {
                isOpen = -1;
                return;
              }
            }}
          >
            <!-- {#if !item.disable}
              {item.id - 4}
            {/if} -->
          </div>
        {:else}
          <!-- svelte-ignore a11y-click-events-have-key-events -->
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <div
            style="background-color: {item.color};"
            class="absolute top-0 left-0 w-full h-full bg-zinc-900 rounded-md p-2 z-10 overflow-y-scroll no-scrollbar"
            in:receive|global={{ key: item.id, duration: 300 }}
            out:send|global={{ key: item.id, duration: 300 }}
          >
            <div>
              <div class="flex justify-between items-center rounded-lg px-1">
                <button
                  on:click={() => {
                    isOpen = -1;
                  }}
                  class="border px-2.5 py-0.5 border-background bg-background/5 rounded-full"
                  >Back</button
                >
                <button
                  on:click={() => {
                    isOpen = -1;
                  }}
                  class=" px-2.5 py-0.5"
                >
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="16"
                    height="16"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    class="lucide lucide-square-arrow-out-up-right"
                    ><path
                      d="M21 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h6"
                    /><path d="m21 3-9 9" /><path d="M15 3h6v6" /></svg
                  >
                </button>
              </div>
              <div class="mt-1.5">
                <img
                  in:fly={{ y: 15, x: 15, duration: 200, delay: 130 }}
                  src={item.img}
                  class="border-2 border-white rounded-xl w-full h-44 object-cover object-center"
                  alt="doodle"
                />
              </div>
              <div class="mt-1 px-1 mb-2">
                <h3 class="text-lg font-bold text-neutral-900">
                  {item.text}
                </h3>
                <p class="text-neutral-800">{item.desc}</p>
              </div>
            </div>
          </div>
        {/if}
      {/each}
    </div>
  </div>
</div>
