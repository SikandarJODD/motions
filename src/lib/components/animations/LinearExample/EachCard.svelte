<script lang="ts">
  import { AnimatePresence, AnimateSharedLayout, Motion } from "svelte-motion";

  let isOpen = false;
  let onClickHandler = () => {
    isOpen = !isOpen;
  };
  interface InitialValuesTypes {
    id: number;
    img: string;
    title: string;
    description: string;
  }
  export let value: InitialValuesTypes;
</script>

<AnimateSharedLayout>
  <div class="grow basis-[300px]">
    <AnimatePresence let:item list={[{ key: value.id }]}>
      {#if isOpen}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <Motion layoutId={`wrapper-${value.id}`} let:motion>
          <div
            on:click={onClickHandler}
            class="fixed left-0 top-0 flex h-full w-full items-end"
          >
            <Motion
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              exit={{ opacity: 0 }}
              let:motion
            >
              <div
                class="pointer-events-none absolute inset-0 -z-20 bg-black/20 backdrop-blur-md"
                use:motion
              ></div>
            </Motion>

            <!-- Main Container -->
            <div
              class="mx-auto h-[93dvh] z-[1000] w-full max-w-4xl overflow-auto bg-black"
              style="border-radius:24px 24px 0px 0px;"
              use:motion
            >
              <Motion layoutId={`image-${value.id}`} let:motion>
                <img
                  use:motion
                  src={value.img}
                  width={400}
                  height={400}
                  alt=""
                  class="mx-auto w-full"
                />
              </Motion>
              <div class="relative z-50 mx-auto mt-[-200px] max-w-2xl pb-12">
                <Motion layoutId={`title-${value.id}`} let:motion>
                  <h2
                    use:motion
                    class="relative inline-block max-w-[600px] text-[56px] font-medium"
                  >
                    {value.title}
                  </h2>
                  <p class="mt-8 text-[15px] text-[#969799]">
                    {value.description}
                  </p>
                </Motion>
              </div>
            </div>
          </div>
        </Motion>
      {:else}
        <Motion let:motion layoutId={`wrapper-${value.id}`}>
          <button
            use:motion
            style="transition: filter 200ms;"
            class="h-full w-full overflow-hidden bg-zinc-950 hover:brightness-125 rounded-[24px]"
            on:click={onClickHandler}
          >
            <Motion layoutId={`image-${value.id}`} let:motion>
              <img
                use:motion
                src={value.img}
                width={400}
                height={400}
                alt=""
                class="mx-auto w-[280px]"
              />
            </Motion>
            <span
              class="flex items-center justify-between gap-4 p-6 pr-8 text-start"
            >
              <Motion layoutId={`title-${value.id}`} let:motion>
                <h2 use:motion class="text-[21px]">
                  {value.title}
                </h2>
              </Motion>
              <div
                class="flex h-8 w-8 items-center justify-center rounded-full border border-white/20"
                style="flex: 0 0 auto;"
              >
                <svg
                  width="16"
                  height="16"
                  viewBox="0 0 16 16"
                  fill="#9c9da1"
                  role="img"
                  focusable="false"
                  aria-hidden="true"
                >
                  <path
                    d="M8.75 4C8.75 3.58579 8.41421 3.25 8 3.25C7.58579 3.25 7.25 3.58579 7.25 4V7.25H4C3.58579 7.25 3.25 7.58579 3.25 8C3.25 8.41421 3.58579 8.75 4 8.75H7.25V12C7.25 12.4142 7.58579 12.75 8 12.75C8.41421 12.75 8.75 12.4142 8.75 12V8.75H12C12.4142 8.75 12.75 8.41421 12.75 8C12.75 7.58579 12.4142 7.25 12 7.25H8.75V4Z"
                  ></path>
                </svg>
              </div>
            </span>
          </button>
        </Motion>
      {/if}
    </AnimatePresence>
  </div>
</AnimateSharedLayout>
