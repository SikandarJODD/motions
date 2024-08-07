<script>
  import { Motion, MotionConfig, AnimateSharedLayout } from "svelte-motion";
  import ItemsButton from "./ItemsButton.svelte";
  let isOpen = false;
  let onIconClickHandler = () => {
    isOpen = !isOpen;
  };
</script>

<AnimateSharedLayout type="crossfade">
  <MotionConfig
    transition={{
      type: "spring",
      bounce: 0.2,
      duration: 0.5,
    }}
  >
    {#if isOpen}
      <Motion let:motion layoutId="wrapper">
        <div
          use:motion
          class="relative w-full max-w-96 overflow-hidden border border-border bg-[#161716] p-2 rounded-[12px]"
        >
          <ItemsButton {isOpen} on:click={onIconClickHandler} />
        </div>
      </Motion>
    {:else}
      <Motion let:motion layoutId="wrapper">
        <button
          on:click={onIconClickHandler}
          use:motion
          class="group flex h-12 w-32 items-center justify-center gap-1 border border-border bg-[#161716] p-2 active:bg-[#222422] rounded-[14px]"
        >
          <Motion layoutId="add-style-text" let:motion>
            <span
              class="inline-block text-[#929292] group-hover:text-white"
              use:motion>Add Style</span
            >
          </Motion>
          <Motion layoutId="action-button" let:motion>
            <svg
              use:motion
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
          </Motion>
        </button>
      </Motion>
    {/if}
  </MotionConfig>
</AnimateSharedLayout>
