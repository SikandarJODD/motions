<script>
  import { cn } from "$lib/utils";
  import { QrCode, Hourglass, TriangleAlert } from "lucide-svelte";
  import { Motion, MotionConfig, AnimatePresence } from "svelte-motion";

  let isOpen = false;
  let isSending = false;
  let isError = false;
  let onClickHandler = () => {
    isOpen = !isOpen;
    isSending = false;
    isError = false;
  };
  let onSendingHandler = async () => {
    isSending = !isSending;
    await new Promise((resolve) => setTimeout(resolve, 2000));
    isError = true;
    isSending = false;
  };
</script>

<div
  class="flex h-full min-h-dvh w-full items-center justify-center bg-[#1C1A1B] text-white"
>
  <!-- Iphone stuff -->
  <div
    class="relative isolate h-[600px] w-[360px] overflow-auto py-12 rounded-[28px] border"
  >
    <div
      style="background: radial-gradient(50% 50% at 50% 50%, #FF6B00 0%, rgba(255, 153, 0, 0.48) 49%, rgba(255, 153, 0, 0.00) 100%);"
      class="absolute left-0 top-0 -z-10 h-96 w-96 -translate-x-1/2 -translate-y-1/2 blur-3xl"
    ></div>
    <AnimatePresence let:item list={[{ key: isOpen }]}>
      {#if isOpen}
        <Motion
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          exit={{ opacity: 0 }}
          let:motion
        >
          <div
            class="absolute inset-0 -z-10 bg-black/50 backdrop-blur-3xl"
            use:motion
          ></div>
        </Motion>
      {/if}
    </AnimatePresence>
    <div class="flex h-full flex-col justify-end px-4 pb-4">
      <button
        class="h-14 w-full rounded-2xl bg-[#1E1E1E] duration-200 active:scale-90"
        on:click={onClickHandler}
      >
        {#if isError}
          Okay
        {:else if isOpen}
          Cancel
        {:else}
          Open
        {/if}
      </button>
      <MotionConfig transition={{ duration: 0.5, type: "spring", bounce: 0 }}>
        {#if isOpen}
          <!-- <AnimatePresence initial={false} let:item list={[{ key: isOpen }]}> -->
          <Motion
            initial={{ opacity: 0, y: -30 }}
            animate={{ opacity: 1, y: -80 }}
            exit={{ opacity: 0, y: -30 }}
            let:motion
          >
            <div class="absolute left-0 w-full -translate-y-20 px-4" use:motion>
              <Motion
                animate={{
                  background: isError
                    ? "linear-gradient(to bottom, #FE0557 2%, #1E1E1E 50%)"
                    : "linear-gradient(to bottom, #424242, #1E1E1E)",
                }}
                layout
                let:motion
              >
                <div class="rounded-[24px]" use:motion>
                  <Motion layout let:motion>
                    <div
                      class="rounded-[24px] relative flex h-full min-h-[250px] w-full flex-col items-center justify-center overflow-hidden bg-[#1E1E1E] px-2 pb-4 pt-8"
                      use:motion
                    >
                      {#if isError}
                        <Motion
                          initial={{ opacity: 0 }}
                          animate={{ opacity: 1 }}
                          let:motion
                        >
                          <div
                            class="absolute top-0 h-1/2 w-full scale-125 bg-gradient-to-t from-transparent to-[#FE0557]/50 blur-xl"
                            use:motion
                          ></div>
                        </Motion>
                      {/if}

                      <Motion
                        animate={{
                          background: isError ? "#FE0557" : "#1E1E1E",
                          borderColor: isError ? "#FE0557" : "#424242",
                        }}
                        let:motion
                      >
                        <div
                          class="relative mb-2 flex h-24 w-24 items-center justify-center rounded-full border-2 border-[#424242] text-4xl"
                          use:motion
                        >
                          {#if isSending}
                            <Motion
                              initial={{ opacity: 0 }}
                              animate={{ opacity: 1 }}
                              transition={{ duration: 0.2, type: "tween" }}
                              let:motion
                            >
                              <span class="text-2xl" use:motion>
                                <Hourglass />
                              </span>
                            </Motion>
                          {:else if isError}
                            <Motion
                              initial={{ opacity: 0 }}
                              animate={{ opacity: 1 }}
                              transition={{ duration: 0.2, type: "tween" }}
                              let:motion
                            >
                              <span class="text-2xl" use:motion>
                                <TriangleAlert />
                              </span>
                            </Motion>
                          {:else}
                            <Motion
                              initial={{ opacity: 0 }}
                              animate={{ opacity: 1 }}
                              transition={{ duration: 0.2, type: "tween" }}
                              let:motion
                            >
                              <span use:motion>
                                <QrCode width={36} height={36} />
                              </span>
                            </Motion>
                          {/if}
                        </div>
                      </Motion>

                      {#if !isSending && !isError}
                        <h3 class="mb-2 mt-6 text-2xl">New code</h3>
                        <p
                          class="max-w-[200px] text-center text-sm text-[#7F7F7F]"
                        >
                          how do you want to receive your verification code?
                        </p>

                        <button
                          class="mt-6 h-14 w-full rounded-2xl bg-[#343434] duration-200 active:scale-90"
                          on:click={onSendingHandler}
                        >
                          Text message
                        </button>
                        <button
                          class="mt-2 h-14 w-full rounded-2xl bg-[#343434] duration-200 active:scale-90"
                          on:click={onSendingHandler}
                        >
                          Call my number
                        </button>
                      {/if}

                      {#if isError}
                        <Motion
                          initial={{ opacity: 0 }}
                          animate={{ opacity: 1 }}
                          transition={{ delay: 0.3 }}
                          let:motion
                        >
                          <div
                            class="flex flex-col items-center justify-center"
                            use:motion
                          >
                            <h3 class="mb-2 mt-6 text-2xl">
                              Authentication error
                            </h3>
                            <p
                              class="mb-4 max-w-[200px] text-center text-sm text-[#7F7F7F]"
                            >
                              how do you want to receive your verification code?
                            </p>
                          </div>
                        </Motion>
                      {/if}
                    </div>
                  </Motion>
                </div>
              </Motion>
            </div>
          </Motion>
          <!-- </AnimatePresence> -->
        {/if}
      </MotionConfig>
    </div>
  </div>
</div>
