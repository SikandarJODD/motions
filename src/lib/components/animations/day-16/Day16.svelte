<script lang="ts">
  import { Motion } from "svelte-motion";
  let selectedInput = 0;
  let success = false;
  let ready = false;
  let inputCode = (node: HTMLElement) => {
    node.addEventListener("input", (e: any) => {
      if (e.inputType === "deleteContentBackward") {
        return;
      }
      let nodeId = Number(node.id);
      if (nodeId === 4) {
        selectedInput = 0;
        node.blur();
        ready = true;
        return;
      }
      let ele = document.getElementById(`${nodeId + 1}`);
      if (ele) {
        ele.focus();
      }
    });
    node.addEventListener("focus", (e) => {
      console.log(e, node.id, "plus");
      selectedInput = Number(node.id);
    });
  };
</script>

  <div
    class="relative border border-primary/50 bg-neutral-200 rounded-2xl flex flex-col items-center justify-center px-12 py-24 shadow-lg text-black w-full md:w-96 h-fit"
  >
    <Motion let:motion>
      <div
        use:motion
        class="relative z-50 flex h-24 w-24 items-center justify-center gap-2"
      >
        <Motion
          animate={{
            transform: `
        perspective(300px) 
        rotateY(${selectedInput === 0 ? "0deg" : selectedInput === 1 ? "-20deg" : selectedInput === 2 ? "-10deg" : selectedInput === 3 ? "10deg" : selectedInput === 4 ? "20deg" : ""})
        rotateX(${selectedInput === 0 ? "0deg" : "-10deg"})
        `,
          }}
          let:motion
        >
          <div
            use:motion
            class="absolute inset-0 -z-10 rounded-3xl bg-black"
          ></div>
        </Motion>
        <Motion
          animate={{
            scale:
              selectedInput === 0
                ? 1
                : selectedInput === 1
                  ? 0.8
                  : selectedInput === 2
                    ? 0.9
                    : selectedInput === 3
                      ? 1
                      : selectedInput === 4
                        ? 1.15
                        : 1,
          }}
          let:motion
        >
          <div use:motion class="text-3xl text-white">
            <svg
              stroke="currentColor"
              fill="currentColor"
              stroke-width="0"
              viewBox="0 0 256 256"
              height="30px"
              width="30px"
              xmlns="http://www.w3.org/2000/svg"
              ><path
                d="M240,128a15.79,15.79,0,0,1-10.5,15l-63.44,23.07L143,229.5a16,16,0,0,1-30,0L89.94,166.06,26.5,143a16,16,0,0,1,0-30L89.94,89.94,113,26.5a16,16,0,0,1,30,0l23.07,63.44L229.5,113A15.79,15.79,0,0,1,240,128Z"
              ></path></svg
            >
            <!-- <PiStarFourFill /> -->
          </div>
        </Motion>
        <Motion
          animate={{
            scale:
              selectedInput === 0
                ? 1
                : selectedInput === 1
                  ? 1.15
                  : selectedInput === 2
                    ? 1
                    : selectedInput === 3
                      ? 0.9
                      : selectedInput === 4
                        ? 0.8
                        : "",
          }}
          let:motion
        >
          <div use:motion class="text-3xl text-white">
            <svg
              stroke="currentColor"
              fill="currentColor"
              stroke-width="0"
              viewBox="0 0 256 256"
              height="30px"
              width="30px"
              xmlns="http://www.w3.org/2000/svg"
              ><path
                d="M240,128a15.79,15.79,0,0,1-10.5,15l-63.44,23.07L143,229.5a16,16,0,0,1-30,0L89.94,166.06,26.5,143a16,16,0,0,1,0-30L89.94,89.94,113,26.5a16,16,0,0,1,30,0l23.07,63.44L229.5,113A15.79,15.79,0,0,1,240,128Z"
              ></path></svg
            >
            <!-- <PiStarFourFill /> -->
          </div>
        </Motion>
      </div>
    </Motion>
    <div class="mt-12 flex gap-2">
      {#each { length: 4 } as _, index}
        <div
          class="relative {selectedInput - 1 === index
            ? 'border border-purple-500'
            : ''} 0 flex h-14 w-11 items-center justify-center rounded-2xl shadow-lg"
        >
          <input
            type="text"
            use:inputCode
            id={String(index + 1)}
            class="h-full w-full bg-transparent text-center text-xl font-medium outline-none"
          />
          <Motion
            initial={{ opacity: 0, padding: 0 }}
            animate={{
              opacity: selectedInput === index + 1 ? 1 : 0,
              padding: selectedInput === index + 1 ? 2 : 0,
            }}
            let:motion
          >
            <div
              class="pointer-events-none absolute inset-0 -z-10 overflow-hidden rounded-2xl bg-transparent bg-violet-500"
              use:motion
            >
              <div class="h-full w-full rounded-[14px] bg-white"></div>
            </div>
          </Motion>
        </div>
      {/each}
    </div>
    <Motion>
      <button
        on:click={() => {
          success = true;
        }}
        class="relative isolate mt-12 h-14 w-full overflow-hidden rounded-full bg-[#F2F2F4] duration-200 hover:scale-95 active:scale-90 {ready
          ? 'text-white'
          : 'text-[#D0CFD9]'}"
      >
        Connect
        {#if ready}
          <Motion initial={{ opacity: 0 }} animate={{ opacity: 1 }} let:motion>
            <div
              style="background: linear-gradient(90deg, #8355FF 0%, #A480FF 50%, #8355FF 100%)"
              use:motion
              class="absolute inset-0 -z-10"
            ></div>
          </Motion>
        {/if}
      </button>
    </Motion>
  </div>
