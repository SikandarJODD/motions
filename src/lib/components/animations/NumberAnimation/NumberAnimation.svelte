<script>
    import { onDestroy } from "svelte";
    import { Motion } from "svelte-motion";
  import Wrapper from "../Wrapper.svelte";
  
    const randNumber = [
      Math.floor(Math.random() * 10),
      Math.floor(Math.random() * 10),
      Math.floor(Math.random() * 10),
      Math.floor(Math.random() * 10),
      Math.floor(Math.random() * 10),
      Math.floor(Math.random() * 10),
    ];
    let explode = false;
    let currentIndex = 0;
    let internal;
  
    // Reactive statement that triggers when `currentIndex` changes
    $: {
      if (currentIndex === 5) {
        setTimeout(() => {
          explode = true;
        }, 400);
      } else {
        clearInterval(internal);
        internal = setInterval(() => {
          currentIndex += 1;
        }, 500);
      }
    }
  
    // Cleanup when the component is destroyed
    onDestroy(() => {
      clearInterval(internal);
    });
  </script>
  
  <!-- <Wrapper> -->
    <div
      class="flex h-96 w-full max-w-lg items-center justify-center gap-3 rounded-3xl bg-[rgba(33,33,38)]"
    >
      {#each randNumber as num, index (index)}
        <div class="relative">
          <div
            class="custom_shadow flex h-10 w-8 items-center justify-center rounded-md bg-[rgba(19,19,22)]"
          >
            {#if index <= currentIndex}
              <Motion
                initial={{ y: 2, opacity: 0 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ delay: 0.3 }}
                let:motion
              >
                <p class="text-white" use:motion>{num}</p>
              </Motion>
            {/if}
          </div>
          {#if index === currentIndex && !explode}
            <Motion
              layoutId="number-animation"
              initial={{ scale: 1.8 }}
              animate={{ scale: 1 }}
              transition={{
                duration: 0.3,
                type: "spring",
              }}
              let:motion
            >
              <div
                class="absolute inset-0 flex justify-center rounded-md border-2 border-cyan-600/50 bg-cyan-500/10"
                use:motion
              >
                <div class="absolute bottom-0.5 h-px w-1/2 bg-cyan-600"></div>
              </div>
            </Motion>
          {/if}
          {#if explode}
            <Motion
              initial={{ scale: 1, opacity: 1 }}
              animate={{ scale: 1.5, opacity: 0 }}
              transition={{
                duration: 0.3,
                type: "tween",
              }}
              let:motion
            >
              <div
                class="absolute inset-0 flex justify-center rounded-md border-2 border-cyan-600/50 bg-cyan-500/10"
                use:motion
              >
                <div class="absolute bottom-0.5 h-px w-1/2 bg-cyan-600"></div>
              </div>
            </Motion>
          {/if}
        </div>
      {/each}
    </div>
  <!-- </Wrapper> -->
  