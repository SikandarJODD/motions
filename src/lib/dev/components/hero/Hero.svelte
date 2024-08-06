<script>
  import Button from "$lib/components/ui/button/button.svelte";
  import AnimatedShinyText from "$lib/components/ui/magic/AnimatedShinyText/AnimatedShinyText.svelte";
</script>

<div class="flex items-center h-[70vh] w-full justify-center flex-col px-2 md:px-0">
  <div class="mb-5">
    <AnimatedShinyText class="border border-neutral-500 px-3 py-1 rounded-full"
      >🪄 Introducing Motions
    </AnimatedShinyText>
  </div>
  <h1
    class="text-3xl font-bold md:text-5xl bg-gradient-to-br from-white to-neutral-500 text-transparent bg-clip-text"
  >
    Svelte Motions
  </h1>
  <p class="mt-3 text-lg text-muted-foreground  text-center">
    Amazing animations build using Svelte & Svelte Motions
  </p>
  <div class="mt-6">
    <Button class="rounded-full">Get Started</Button>
  </div>
</div>
