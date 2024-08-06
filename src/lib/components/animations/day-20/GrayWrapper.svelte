<script>
    import { Motion } from "svelte-motion";
    export let isHover = false;
  </script>
  
  <Motion initial={{ x: 16 }} animate={{ x: isHover ? 32 : 16 }} let:motion>
    <div
      class="flex h-16 w-72 translate-x-4 items-center gap-4 rounded-lg border-[#262626] bg-[#1D1D1D] pl-4"
      use:motion
    >
      <slot></slot>
    </div>
  </Motion>
  