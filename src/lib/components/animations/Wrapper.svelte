<script>
  import { cn } from "$lib/utils";
  let className = "";
  export { className as class };
</script>

<div
  class={cn(
    "relative flex min-h-dvh w-full flex-col items-center justify-center bg-white text-black",
    className
  )}
  {...$$restProps}
>
  <slot></slot>
</div>
