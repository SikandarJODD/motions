<script>
  import { cn } from "$lib/utils";
  import { PencilLine } from "lucide-svelte";
  import { AnimatePresence, Motion, MotionConfig } from "svelte-motion";
  import Date from "./Date.svelte";
  import { onMount } from "svelte";
  let isOpen = false;
  let editDate = false;
  let buttons = [
    "open-card",
    "edit-label",
    "change-member",
    "change-cover",
    "edit-dates",
    "move",
    "copy",
    "archive",
  ];

  let onEditClickHandler = () => {
    isOpen = !isOpen;
    setTimeout(() => {
      onResize();
    }, 10);
  };
  let onEditDateClickHandler = () => {
    editDate = !editDate;
    setTimeout(() => {
      onResize();
    }, 10);
  };
  let height = 0;
  let element;
  let onResize = () => {
    height = element.offsetHeight;
  };
  onMount(() => {
    onResize();
  });
</script>

<MotionConfig transition={{ duration: 0.5, type: "spring", bounce: 0 }}>
  <Motion
    animate={{
      zIndex: isOpen ? 30 : 0,
      transition: { zIndex: { delay: isOpen ? 0 : 0.4 } },
    }}
    let:motion
  >
    <div class={cn("relative h-[110px]")} use:motion>
      <Motion animate={{ height }} let:motion>
        <div
          class="group absolute left-0 top-0 w-full overflow-hidden rounded-2xl bg-white"
          use:motion
        >
          <div bind:this={element} class="p-6">
            <AnimatePresence let:item list={[{ key: "code" }]}>
              {#if !editDate}
                <Motion
                  initial={{ x: "-120%" }}
                  animate={{ x: 0 }}
                  exit={{ x: "-120%" }}
                  let:motion
                >
                  <div use:motion>
                    <h2 class="font-bold">Define Requirements</h2>
                    <p
                      class={cn(
                        "mt-1 text-sm leading-[1.1rem] text-[#B0B0B2]",
                        isOpen && "mb-6"
                      )}
                    >
                      Gather and document all project specifications from
                      stakeholders.
                    </p>
                    <AnimatePresence let:item list={[{ key: "Save" }]}>
                      {#if isOpen}
                        <Motion
                          initial={{ y: 40 }}
                          animate={{ y: 0 }}
                          exit={{ y: 40 }}
                          let:motion
                        >
                          <button
                            class="h-12 w-full rounded-lg bg-gradient-to-b from-[#323434] to-black text-white"
                            use:motion
                            on:click={onEditClickHandler}
                          >
                            {item.key}
                          </button>
                        </Motion>
                      {/if}
                    </AnimatePresence>
                  </div>
                </Motion>
              {:else}
                <Motion
                  initial={{ x: "120%" }}
                  animate={{ x: 0 }}
                  exit={{ x: "120%" }}
                  let:motion
                >
                  <div use:motion>
                    <Date
                      on:click={() => {
                        editDate = false;
                        setTimeout(() => {
                          onResize();
                        }, 10);
                      }}
                    />
                  </div>
                </Motion>
              {/if}
            </AnimatePresence>
            {#if !isOpen}
              <button
                class="absolute right-2 top-2 rounded-md p-1 opacity-0 duration-100 hover:bg-[#EAEAEA] group-hover:opacity-100"
                on:click={onEditClickHandler}
              >
                <PencilLine class="w-4 h-4 transition-all duration-500" />
              </button>
            {/if}
          </div>
        </div>
      </Motion>
      <AnimatePresence let:item list={[{ key: "editDate" }]}>
        {#if isOpen && !editDate}
          <Motion
            initial={{ y: 10, x: "var(--x-initial)" }}
            animate={{ y: 0 }}
            exit={{ opacity: 0, scale: 0.9 }}
            let:motion
          >
            <div
              class="absolute right-4 top-0 flex origin-bottom flex-col items-start [--x-initial:calc(100%+30px)]"
              use:motion
            >
              {#each buttons as button}
                <button
                  on:click={onEditDateClickHandler}
                  class="mb-2 h-10 rounded-lg border-t-[.8px] border-[#9A9A9E] bg-[#828286] px-4 text-lg capitalize text-white hover:bg-[#6a6a6e]"
                >
                  {button.replaceAll("-", " ")}
                </button>
              {/each}
            </div>
          </Motion>
        {/if}
      </AnimatePresence>
    </div>
  </Motion>
</MotionConfig>

<AnimatePresence let:item list={[{ key: "wrapper" }]}>
  {#if isOpen}
    <Motion
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
      let:motion
    >
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <div
        use:motion
        class="absolute left-0 top-0 z-20 h-full w-full bg-black/70 backdrop-blur-sm"
        on:click={() => {
          if (!editDate) {
            onEditClickHandler();
          }
        }}
      ></div>
    </Motion>
  {/if}
</AnimatePresence>
