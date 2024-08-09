<script lang="ts">
  import { onMount } from "svelte";
  import { cn } from "$lib/utils";
  import { MotionConfig, Motion, AnimateSharedLayout } from "svelte-motion";

  $: filter = false;
  let onClickHandler = () => {
    setTimeout(() => {
      calcHeight();
    }, 100);
    filter = !filter;
  };
  type sportsTypes = Record<string, boolean>;
  let sportsObject: sportsTypes = {
    Soccer: false,
    Basketball: false,
    Baseball: false,
    Tennis: true,
    Golf: false,
    Cricket: false,
    Rugby: false,
    Hockey: false,
    "Table Tennis": false,
    Badminton: false,
    Volleyball: false,
    "American Football": false,
    Boxing: false,
    MMA: false,
    Wrestling: false,
    Swimming: false,
    Athletics: false,
    Cycling: false,
    Gymnastics: false,
    Skiing: false,
    Snowboarding: false,
    Skateboarding: false,
    Surfing: false,
    Rowing: false,
    Sailing: false,
    Fencing: false,
    Judo: true,
    Karate: false,
    Taekwondo: false,
    Archery: false,
    Equestrian: false,
    Lacrosse: false,
    Handball: false,
    Softball: false,
    Squash: false,
    Racquetball: false,
    Bobsleigh: false,
    Curling: false,
    "Figure Skating": false,
    Diving: false,
  };
  let height = 0;
  let element;
  let calcHeight = () => {
    if (element) {
      console.log(element.offsetHeight);
      height = element.offsetHeight;
    }
  };
  onMount(() => {
    calcHeight();
  });
</script>

<div class="flex h-dvh w-full items-center justify-center bg-[#0E0C0E] px-4">
  <div class="w-full max-w-4xl">
    <h1 class="text-xl font-bold tracking-tight">
      What are your favorite language?
    </h1>
    <MotionConfig
      transition={{
        duration: 0.7,
        type: "spring",
        bounce: filter ? 0 : undefined,
      }}
    >
      <Motion
        initial={{ height: "auto" }}
        animate={{ height: height > 0 ? height : undefined }}
        let:motion
      >
        <div use:motion>
          <Motion let:motion>
            <ul
              bind:this={element}
              class="mt-4 flex w-full flex-wrap gap-2"
              use:motion
            >
              <AnimateSharedLayout>
                <!-- <AnimatePresence let:item list={[{ key: 'a'}]}> -->
                {#each Object.entries(sportsObject).filter(([key, value]) => !filter || value) as item, i}
                  <Motion
                    layout="position"
                    initial={{ opacity: 0 }}
                    animate={{ opacity: 1, transition: { delay: 0.2 } }}
                    exit={{ opacity: 0, transition: { duration: 0.1 } }}
                    let:motion
                  >
                    <li
                      use:motion
                      style="
                    transition: width 0.3s;
                  "
                    >
                      <Motion layout let:motion>
                        <button
                          class={cn(
                            "flex h-10 w-fit transition-all duration-700 items-center gap-2 border border-[#373538] bg-[#161417] px-4 text-[#A3A1A3]",
                            item[1] &&
                              "border-[#452C28] bg-[#1C1210] text-[#EA885A]"
                          )}
                          style="border-radius: 9999px; transition: width 0.8s;"
                          on:click={() => {
                            sportsObject[item[0]] = !sportsObject[item[0]];
                          }}
                          use:motion
                        >
                          <Motion layout let:motion>
                            <span use:motion class="inline-block">
                              {item[0]}
                            </span>
                          </Motion>
                          {#if item[1]}
                            <Motion
                              initial={{ scale: 0 }}
                              animate={{ scale: 1 }}
                              let:motion
                            >
                              <span use:motion>
                                <svg
                                  xmlns="http://www.w3.org/2000/svg"
                                  width="16"
                                  height="16"
                                  viewBox="0 0 24 24"
                                  fill="none"
                                  stroke="currentColor"
                                  stroke-width="1.4"
                                  stroke-linecap="round"
                                  stroke-linejoin="round"
                                  class="lucide lucide-circle-check"
                                  ><circle cx="12" cy="12" r="10" /><path
                                    d="m9 12 2 2 4-4"
                                  /></svg
                                >
                              </span>
                            </Motion>
                          {/if}
                        </button>
                      </Motion>
                    </li>
                  </Motion>
                {/each}
                <!-- </AnimatePresence> -->
              </AnimateSharedLayout>
            </ul>
          </Motion>
        </div>
      </Motion>
    </MotionConfig>

    <div class="flex justify-center py-8">
      <button
        class="h-8 rounded border border-[#452C28] bg-[#1C1210] px-4 text-[#EA885A] duration-200 active:scale-95"
        on:click={onClickHandler}
      >
        Submit
      </button>
    </div>
  </div>
</div>
