<script lang="ts">
  import { onMount, tick } from "svelte";
  import RabitAiImg from "$lib/imgs/rabbit-ai.png";
  import {
    MotionConfig,
    Motion,
    AnimateSharedLayout,
  } from "svelte-motion";
  let isOpen = false;
  let element: HTMLElement;
  let height = 0;
  onMount(() => {
    if (element) {
      height = element.clientHeight;
      // console.log("close", element.getBoundingClientRect());
    }
  });

  let onClickHandler = async () => {
    isOpen = !isOpen;
    await tick();
    if (element) {
      height = element.clientHeight;
    }
  };
</script>

<AnimateSharedLayout type="crossfade">
  <MotionConfig transition={{ duration: 0.5, type: "spring", bounce: 0 }}>
    <Motion animate={{ height: height > 0 ? height : undefined }} let:motion>
      <div class=" rounded-2xl bg-[#F5F5F5] text-black overflow-hidden" use:motion>
        <div
          bind:this={element}
          class="flex w-full md:w-[400px] flex-col items-center p-1"
        >
          <Motion
            layout
            animate={{ background: isOpen ? "#ffffff" : "#F5F5F5" }}
            let:motion
          >
            <div
              use:motion
              class="grid w-full grid-cols-5 items-center rounded-2xl p-3"
            >
              <Motion layoutId="img-layout" let:motion>
                <img
                  use:motion
                  src={RabitAiImg}
                  alt="rabbit-ai"
                  class="z-20 w-[80px]"
                />
              </Motion>
              <div class="col-span-3">
                <!-- <AnimatePresence let:item list={[{ key: crypt }]}> -->
                <div class="flex font-bold">
                  <Motion layoutId="h2-layout" let:motion>
                    <h2 class="tracking-tight" use:motion>Rabbit R1</h2>
                  </Motion>
                  {#if isOpen}
                    <Motion layoutId="h2-layout" let:motion>
                      <h2 class="text-center" use:motion>Rabbit R1</h2>
                    </Motion>
                  {/if}
                </div>
                <!-- </AnimatePresence> -->
                {#if isOpen}
                  <Motion layoutId="img-layout" let:motion>
                    <img
                      use:motion
                      src={RabitAiImg}
                      alt="rabbit-ai"
                      class="mx-auto w-[130px]"
                    />
                  </Motion>
                {/if}
                <Motion layout let:motion>
                  <div
                    use:motion
                    class="flex text-sm font-normal text-[#A1A1A1]
                      {!isOpen ? 'divide-x divide-[#E2E2E2]' : ''}
                      "
                  >
                    <p class="pr-2">
                      <Motion let:motion layoutId="1-layout">
                        <span use:motion class="inline-block">1</span>
                      </Motion>
                      <Motion let:motion layoutId="piece-layout">
                        <span use:motion class="inline-block">piece</span>
                      </Motion>
                    </p>
                    <!-- another p -->
                    <p class="px-2">
                      <Motion let:motion layoutId="$-layout">
                        <span use:motion class="inline-block">$</span>
                      </Motion>
                      <Motion let:motion layoutId="89-layout">
                        <span use:motion class="inline-block">89</span>
                      </Motion>
                    </p>
                    <!-- another p -->
                    <p class="px-2">
                      <Motion let:motion layoutId="36645-layout">
                        <span use:motion class="inline-block">36645</span>
                      </Motion>
                    </p>
                  </div>
                </Motion>
              </div>
              <Motion layout let:motion>
                <div
                  use:motion
                  class="flex flex-col items-end justify-center gap-2"
                >
                  <button
                    class="flex h-7 w-7 items-center justify-center rounded-full bg-white"
                    on:click={onClickHandler}
                  >
                    <svg
                      width="15"
                      height="11"
                      viewBox="0 0 15 11"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M14.8734 5.50599C14.8525 5.45868 14.3452 4.33339 13.2175 3.2057C11.7149 1.70311 9.8171 0.908998 7.72821 0.908998C5.63932 0.908998 3.74147 1.70311 2.23889 3.2057C1.1112 4.33339 0.601554 5.46048 0.582989 5.50599C0.555748 5.56726 0.541672 5.63357 0.541672 5.70063C0.541672 5.76768 0.555748 5.83399 0.582989 5.89526C0.603949 5.94257 1.1112 7.06727 2.23889 8.19496C3.74147 9.69694 5.63932 10.4911 7.72821 10.4911C9.8171 10.4911 11.7149 9.69694 13.2175 8.19496C14.3452 7.06727 14.8525 5.94257 14.8734 5.89526C14.9007 5.83399 14.9147 5.76768 14.9147 5.70063C14.9147 5.63357 14.9007 5.56726 14.8734 5.50599ZM7.72821 9.53285C5.88486 9.53285 4.27448 8.86271 2.94137 7.54158C2.3944 6.9976 1.92904 6.37732 1.55976 5.70003C1.9289 5.02265 2.39428 4.40235 2.94137 3.85848C4.27448 2.53735 5.88486 1.8672 7.72821 1.8672C9.57156 1.8672 11.1819 2.53735 12.515 3.85848C13.0631 4.40226 13.5295 5.02255 13.8997 5.70003C13.4679 6.50612 11.5868 9.53285 7.72821 9.53285ZM7.72821 2.82541C7.15966 2.82541 6.60389 2.994 6.13116 3.30987C5.65843 3.62574 5.28998 4.07469 5.07241 4.59996C4.85484 5.12523 4.79791 5.70322 4.90883 6.26084C5.01974 6.81846 5.29353 7.33067 5.69555 7.73269C6.09757 8.13471 6.60978 8.40849 7.1674 8.51941C7.72502 8.63033 8.30301 8.5734 8.82828 8.35583C9.35355 8.13826 9.8025 7.76981 10.1184 7.29708C10.4342 6.82435 10.6028 6.26857 10.6028 5.70003C10.602 4.93787 10.2989 4.20717 9.76 3.66824C9.22107 3.12932 8.49036 2.8262 7.72821 2.82541ZM7.72821 7.61644C7.34918 7.61644 6.97866 7.50404 6.66351 7.29347C6.34836 7.08289 6.10272 6.78358 5.95768 6.43341C5.81263 6.08323 5.77468 5.6979 5.84862 5.32615C5.92257 4.95441 6.10509 4.61293 6.3731 4.34492C6.64112 4.0769 6.98259 3.89438 7.35434 3.82044C7.72608 3.74649 8.11141 3.78445 8.46159 3.92949C8.81177 4.07454 9.11107 4.32017 9.32165 4.63533C9.53223 4.95048 9.64462 5.321 9.64462 5.70003C9.64462 6.20829 9.44271 6.69574 9.08332 7.05513C8.72392 7.41453 8.23647 7.61644 7.72821 7.61644Z"
                        fill="black"
                      />
                    </svg>
                  </button>
                  <button
                    class="flex h-7 w-7 items-center justify-center rounded-full bg-white"
                  >
                    <svg
                      width="14"
                      height="13"
                      viewBox="0 0 14 13"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <line
                        x1="0.0430813"
                        y1="4.2107"
                        x2="13.4133"
                        y2="4.2107"
                        stroke="#060606"
                        stroke-width="1.45864"
                      />
                      <circle
                        cx="9.07162"
                        cy="3.98707"
                        r="1.85832"
                        fill="white"
                        stroke="black"
                        stroke-width="0.345903"
                      />
                      <line
                        x1="0.0430813"
                        y1="9.56476"
                        x2="13.4133"
                        y2="9.56476"
                        stroke="#060606"
                        stroke-width="1.45864"
                      />
                      <circle
                        cx="4.10234"
                        cy="9.468"
                        r="1.8215"
                        fill="white"
                        stroke="black"
                        stroke-width="0.339049"
                      />
                    </svg>
                  </button>
                </div>
              </Motion>
            </div>
          </Motion>
          {#if isOpen}
            <div
              class="mt-4 grid w-full grid-cols-3 divide-x divide-[#E2E2E2] px-8 text-xl font-normal text-[#A1A1A1]"
            >
              <div class="flex flex-col pr-2">
                <div class="h-6">
                  <Motion let:motion layoutId="1-layout">
                    <span use:motion class="absolute inline-block text-black">
                      1
                    </span>
                  </Motion>
                </div>
                {" "}
                <div class="relative h-8">
                  <Motion let:motion layoutId="piece-layout"
                    ><span use:motion class="absolute inline-block text-sm">
                      piece
                    </span>
                  </Motion>
                </div>
              </div>
              <div class="flex flex-col px-2">
                <div class="relative h-6">
                  <Motion let:motion layoutId="89-layout">
                    <span use:motion class="absolute inline-block text-black">
                      89
                    </span>
                  </Motion>
                </div>
                <div class="relative h-8">
                  <Motion let:motion layoutId="cost-layout">
                    <span use:motion class="inline-block text-sm"> Cost </span>
                  </Motion>
                  <Motion let:motion layoutId="$-layout">
                    <span
                      use:motion
                      class="absolute top-[6px] inline-block text-sm"
                    >
                      $
                    </span>
                  </Motion>
                </div>
              </div>
              <div class="flex flex-col px-2">
                <div class="relative h-6">
                  <Motion let:motion layoutId="36645-layout">
                    <span use:motion class="absolute inline-block text-black">
                      36645
                    </span>
                  </Motion>
                </div>
                <div class="relative h-8">
                  <Motion let:motion layoutId="hs-layout">
                    <span use:motion class="inline-block text-sm">
                      HS code</span
                    >
                  </Motion>
                </div>
              </div>
            </div>
          {/if}
        </div>
      </div>
    </Motion>
  </MotionConfig>
</AnimateSharedLayout>
