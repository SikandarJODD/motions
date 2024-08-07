<script>
    import { onMount, tick } from "svelte";
    import { Motion } from "svelte-motion";
  
    let active = "dimensions";
    let changeHeight = false;
    export let isOpen;
    let height = 0;
    let buttons = ["dimensions", "aspect-ratio", "prompt"];
    let element;
    onMount(() => {
      if (element) {
        height = element.clientHeight;
        console.log("close", element.getBoundingClientRect());
      }
    });
  </script>
  
  <Motion layoutId="add-style-text" let:motion>
    <span use:motion class="sr-only pointer-events-none inline-block opacity-0">
      Add Style
    </span>
  </Motion>
  <header class="flex items-center justify-between">
    <Motion
      initial={{ filter: "blur(4px)", opacity: 0 }}
      animate={{ filter: "blur(0px)", opacity: 1 }}
      exit={{ filter: "blur(4px)", opacity: 0 }}
      let:motion
    >
      <div use:motion>
        {#each buttons as button, index}
          <button
            class="relative h-7 px-2 text-sm capitalize outline-none  {button === active
              ? 'text-white'
              : 'text-[#929292]'}"
            on:click={async () => {
              await tick();
              if (element) {
                height = element.clientHeight;
              }
              await new Promise((resolve) => setTimeout(resolve, 1));
              active = button;
              return;
            }}
          >
            <span class="relative z-10">
              {button.replaceAll("-", " ")}
            </span>
            {#if button === active}
              <Motion
                style={{ originY: "0px" }}
                layoutId="header-button-background"
                let:motion
              >
                <div
                  class="pointer-events-none absolute inset-0 rounded bg-[#1D1E1D]"
                  use:motion
                ></div>
              </Motion>
            {/if}
          </button>
        {/each}
      </div>
    </Motion>
    <Motion
      style={{
        rotate: 45,
      }}
      layoutId="action-button"
      let:motion
    >
      <button on:click use:motion class="text-2xl text-[#929292]">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="22"
          height="22"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="1.6"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="lucide lucide-plus"
          ><path d="M5 12h14" /><path d="M12 5v14" /></svg
        >
      </button>
    </Motion>
  </header>
  <Motion
    initial={{ height: "auto" }}
    animate={{ height: changeHeight ? height : undefined }}
    let:motion
  >
    <div use:motion>
      <div bind:this={element}>
        {#if active === "dimensions"}
          <Motion
            initial={{ opacity: 0, filter: "blur(4px)" }}
            animate={{ opacity: 1, filter: "blur(0px)" }}
            let:motion
          >
            <div use:motion>
              <div class="flex h-24 items-center justify-center">Dimensions</div>
              <div class="flex justify-between pl-2 items-center ">
                <small class="flex items-center gap-2 text-[#929292]">
                  <div class="h-1 w-1 rounded-full bg-[#FDFF79]"></div>
                  Changes
                </small>
                <button class="h-8 rounded-md bg-[#FDFF79] px-2 text-black">
                  Apply changes
                </button>
              </div>
            </div>
          </Motion>
        {:else if active === "aspect-ratio"}
          <Motion
            initial={{ opacity: 0, filter: "blur(4px)" }}
            animate={{ opacity: 1, filter: "blur(0px)" }}
            let:motion
          >
            <div use:motion>
              <div class="flex h-20 items-center justify-center">
                Aspect ratio
              </div>
              <div class="flex justify-between pl-2 items-center">
                <small class="flex items-center gap-2 text-[#929292]">
                  <div class="h-1 w-1 rounded-full bg-[#FDFF79]"></div>
                  Changes
                </small>
                <button class="h-8 rounded-md bg-[#FDFF79] px-2 text-black">
                  Apply changes
                </button>
              </div>
            </div>
          </Motion>
        {:else if active === "prompt"}
          <Motion
            initial={{ opacity: 0, filter: "blur(4px)" }}
            animate={{ opacity: 1, filter: "blur(0px)" }}
            let:motion
          >
            <div use:motion>
              <div class="flex h-32 items-center justify-center">Prompt</div>
              <div class="flex justify-between pl-2 items-center">
                <small class="flex items-center gap-2 text-[#929292]">
                  <div class="h-1 w-1 rounded-full bg-[#FDFF79]"></div>
                  Changes
                </small>
                <button class="h-8 rounded-md bg-[#FDFF79] px-2 text-black">
                  Apply changes
                </button>
              </div>
            </div>
          </Motion>
        {/if}
      </div>
    </div>
  </Motion>
  