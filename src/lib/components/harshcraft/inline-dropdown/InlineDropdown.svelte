<script>
  import {
    Pencil,
    Star,
    CloudUpload,
    CopyCheck,
    BellElectric,
    ArrowUpDownIcon,
    Settings,
    Trash2,
    X,
    Check,
  } from "lucide-svelte";
  import { fly } from "svelte/transition";
  let allBts = [
    {
      id: 1,
      name: "New Deployment",
      icon: CloudUpload,
    },
    {
      id: 2,
      name: "Duplicate",
      icon: CopyCheck,
    },
    {
      id: 3,
      name: "Analytics",
      icon: BellElectric,
    },
    {
      id: 4,
      name: "Project",
      icon: ArrowUpDownIcon,
    },
    {
      id: 5,
      name: "Project Settings",
      icon: Settings,
    },
  ];
  import { onMount, onDestroy } from "svelte";

  let holding = false;
  let elapsedTime = 0;
  let maxTime = 2000;
  let timer;

  const handleStart = () => {
    holding = true;
  };

  const handleEnd = () => {
    holding = false;
    elapsedTime = 0;
  };

  const updateElapsedTime = () => {
    elapsedTime = Math.min(elapsedTime + 50, maxTime);
  };

  onMount(() => {
    if (holding) {
      timer = setInterval(updateElapsedTime, 50);
    } else if (!holding && elapsedTime > 0) {
      clearInterval(timer);
    }

    return () => clearInterval(timer);
  });

  $: if (holding) {
    timer = setInterval(updateElapsedTime, 50);
  } else {
    clearInterval(timer);
  }

  $: wPercentage = (elapsedTime / maxTime) * 100;
  let isPastMaxTime = false;
  $: {
    if (elapsedTime >= maxTime) {
      isPastMaxTime = true;
      setTimeout(() => {
        wPercentage = 0;
        isPastMaxTime = false;
        elapsedTime = 0;
        holding = false;
      }, 1000);
    }
  }
  let isFavorite = false;
  let addFavorite = () => {
    isFavorite = !isFavorite;
  };
  let editName = false;
  let inputelement;
  let projectName = "Svelte is Fun";
  let changeName = (e) => {
    allBts[3].name = e.target.value;
  };
</script>

<div
  class="flex w-52 flex-col items-start gap-y-1 rounded-lg border border-neutral-300 bg-neutral-200/10 p-1 dark:border-neutral-700 dark:bg-neutral-800"
>
  <button
    class="relative flex w-full items-center justify-end overflow-hidden rounded px-2 py-1.5 text-xs hover:bg-neutral-950/10 active:bg-neutral-50/15 dark:hover:bg-neutral-50/10"
    on:click={addFavorite}
  >
    {#if isFavorite}
      <span in:fly={{ y: -10, delay: 100 }} class="absolute left-0 ml-2"
        >Add Favorite</span
      >
      <Star class="w-4 h-4" fill="#eee" />
    {:else}
      <span in:fly={{ y: -10 }} class="absolute left-0 ml-2"
        >Remove Favorite</span
      >
      <Star class="w-4 h-4" />
    {/if}
  </button>
  <div
    class="group relative flex h-7 w-full cursor-pointer items-center overflow-hidden rounded text-xs {editName
      ? 'bg-neutral-950/10'
      : 'hover:bg-neutral-950/10'} dark:hover:bg-neutral-50/10"
  >
    {#if !editName}
      <button
        in:fly={{ y: -10 }}
        class="relative flex w-full items-center justify-end overflow-hidden rounded px-2 py-1.5 text-xs hover:bg-neutral-950/10 active:bg-neutral-50/15 dark:hover:bg-neutral-50/10"
        on:click={() => {
          editName = !editName;
          setTimeout(() => {
            inputelement.focus();
            allBts[3].name = projectName;
          }, 200);
        }}
      >
        <span class="absolute left-0 ml-2">Edit Name</span>
        <Pencil class="w-4 h-4" />
      </button>
    {:else}
      <div
        in:fly={{ y: -10 }}
        class="absolute left-0 flex w-full items-center justify-between"
      >
        <input
          bind:this={inputelement}
          bind:value={projectName}
          on:input={changeName}
          type="text"
          class="ml-2 w-4/6 cursor-pointer bg-transparent outline-none"
        />
        <div class="absolute right-0 mr-2 flex items-center gap-x-1">
          <button
            class="rounded bg-neutral-300 p-[3px] text-neutral-700 hover:bg-neutral-400/50 dark:bg-neutral-600 dark:text-neutral-100 dark:hover:bg-neutral-500"
            on:click={() => (editName = false)}
          >
            <Check class="w-3 h-3" strokeWidth="1.2" />
          </button>
          <button
            class="rounded bg-neutral-300 p-[3px] text-neutral-700 hover:bg-neutral-400/50 dark:bg-neutral-600 dark:text-neutral-100 dark:hover:bg-neutral-500"
            on:click={() => (editName = false)}
          >
            <X class="w-3 h-3" strokeWidth="1.2" />
          </button>
        </div>
      </div>
    {/if}
  </div>
  <hr class="w-full border-neutral-300 dark:border-neutral-600" />
  {#each allBts as { name, icon }}
    <button
      class="flex w-full items-center justify-between rounded px-2 py-1.5 text-xs hover:bg-neutral-950/10 active:bg-neutral-50/15 dark:hover:bg-neutral-50/10 transition-all duration-150 group"
    >
      {name}
      <svelte:component
        this={icon}
        class="w-4 h-4 text-muted-foreground group-hover:text-neutral-200"
      />
    </button>
  {/each}
  <hr class="w-full border-neutral-300 dark:border-neutral-600" />
  <button
    class="group relative flex h-7 w-full select-none items-center justify-end overflow-hidden rounded px-2 text-xs text-red-400 hover:bg-red-500/5 dark:hover:bg-red-500/20 outline-none"
    on:mousedown={handleStart}
    on:mouseup={handleEnd}
  >
    <div
      style="width: {wPercentage}%;"
      class="absolute h-full dark:bg-red-500/25 left-0"
    ></div>
    <span class="absolute left-0 ml-2 select-none">
      {#if isPastMaxTime}
        Deleted
      {:else if holding}
        Hold to Confirm
      {:else}
        Delete Project
      {/if}
    </span>
    <Trash2 class="w-4 h-4 text-red-400 group-hover:text-red-500" />
  </button>
</div>
