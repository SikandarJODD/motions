<script>
  import Separator from "$lib/components/ui/magic/Separator/Separator.svelte";
  import Hero from "$lib/dev/components/hero/Hero.svelte";
  import FirstExample from "$lib/dev/components/sections/FirstExample.svelte";
</script>

<Hero />
<div class="px-2 md:px-44">
  <div class="mb-5">
    <Separator gradient={true}>
      <div slot="label" class="border px-4 py-1 rounded-full border-dashed capitalize">
        Motions Examples
      </div>
    </Separator>
  </div>
  <FirstExample />
</div>
