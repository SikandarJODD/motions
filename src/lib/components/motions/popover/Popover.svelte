<script lang="ts">
  import { ArrowLeft } from "lucide-svelte";
  import {
    Motion,
    MotionConfig,
    AnimatePresence,
    AnimateSharedLayout,
  } from "svelte-motion";
  import { fade } from "svelte/transition";
  let transition = {
    type: "spring",
    stiffness: 500,
    damping: 300,
  };
  let uniqueID = crypto.randomUUID().slice(0, 8);
  let isOpen = false;
  let note: string = "";
  let openMenu = () => {
    isOpen = true;
  };
  let closeMenu = () => {
    isOpen = false;
    note = "";
  };
  function clickOutside(node) {
    const handleClick = (event) => {
      if (node && !node.contains(event.target) && !event.defaultPrevented) {
        node.dispatchEvent(new CustomEvent("click_outside", node));
      }
    };

    document.addEventListener("click", handleClick, true);

    return {
      destroy() {
        document.removeEventListener("click", handleClick, true);
      },
    };
  }
</script>

<MotionConfig transition={{ type: "tween", ease: "easeInOut", duration: 0.2 }}>
  <AnimateSharedLayout type="crossfade">
    <div
      class="relative flex items-center justify-center"
      use:clickOutside
      on:click_outside={() => {
        closeMenu();
      }}
    >
      <AnimatePresence let:item list={[{ key: "open" }]}>
        {#if isOpen}
          <Motion layoutId={`popover-${uniqueID}`} let:motion>
            <div
              class="absolute h-[200px] w-[364px] overflow-hidden border border-zinc-950/10 bg-white outline-none dark:bg-zinc-700"
              style="border-radius: 12px;"
              use:motion
            >
              <form class="flex h-full flex-col">
                {#if note.length < 1}
                  <Motion layoutId={`popover-label-${uniqueID}`} let:motion>
                    <span
                      out:fade={{ duration: 200 }}
                      class="absolute left-4 top-3 select-none text-sm text-zinc-500 dark:text-zinc-400"
                      use:motion
                    >
                      Add Note</span
                    >
                  </Motion>
                {/if}

                <textarea
                  class="h-full w-full resize-none rounded-md bg-transparent px-4 py-3 text-sm outline-none"
                  bind:value={note}
                  autofocus
                />
                <div class="flex justify-between px-4 py-3">
                  <button
                    type="button"
                    class="flex items-center"
                    on:click={closeMenu}
                    aria-label="Close popover"
                  >
                    <ArrowLeft
                      size={16}
                      className="text-zinc-900 dark:text-zinc-100"
                    />
                  </button>
                  <button
                    class="relative ml-1 flex h-8 shrink-0 scale-100 select-none appearance-none items-center justify-center rounded-lg border border-zinc-950/10 bg-transparent px-2 text-sm text-zinc-500 transition-colors hover:bg-zinc-100 hover:text-zinc-800 focus-visible:ring-2 active:scale-[0.98] dark:border-zinc-50/10 dark:text-zinc-50 dark:hover:bg-zinc-800"
                    type="button"
                    aria-label="Submit note"
                    on:click={() => {
                      console.log("Send feedback");
                      closeMenu();
                    }}
                  >
                    Submit Note
                  </button>
                </div>
              </form>
            </div>
          </Motion>
        {:else}
          <Motion layoutId={`popover-${uniqueID}`} let:motion>
            <button
              use:motion
              on:click={openMenu}
              class="flex h-9 items-center border border-zinc-950/10 bg-white px-3 text-zinc-950 dark:border-zinc-50/10 dark:bg-zinc-700 dark:text-zinc-50"
              style="border-radius: 8px;"
            >
              <Motion layoutId={`popover-label-${uniqueID}`} let:motion>
                <span class="text-sm" use:motion> Add Note </span>
              </Motion>
            </button>
          </Motion>
        {/if}
      </AnimatePresence>
    </div>
  </AnimateSharedLayout>
</MotionConfig>
