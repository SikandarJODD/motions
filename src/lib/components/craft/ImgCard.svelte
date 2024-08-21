<script>
  import {  onMount } from "svelte";
  import { spring } from "svelte/motion";
  import Button from "../ui/button/button.svelte";

  let state = 0;
  let allimages = [
    "https://i.pinimg.com/564x/36/18/c5/3618c544af9803004da77bf7847ce217.jpg",
    "https://i.pinimg.com/736x/6f/13/10/6f13109fd4e1fcae1a1501a7bf4278d1.jpg",
    "https://i.pinimg.com/736x/2a/68/e6/2a68e6c80713a45c8e57bb6cd034bbb8.jpg",
    "https://i.pinimg.com/564x/c3/dc/c9/c3dcc9dc21bb19e49bb4958273e9213c.jpg",
    "https://i.pinimg.com/564x/ea/f4/78/eaf478176e071e5aa2a0be4539e878b4.jpg",
    "https://i.pinimg.com/564x/85/7d/b1/857db1b59e144d1f301391b67c5f8c8d.jpg",
    "https://i.pinimg.com/564x/4c/46/cd/4c46cda90d2e056b57a01f2102b0a431.jpg",
  ];
  let imgIndex = 0;
  onMount(() => {
    const interval = setInterval(() => {
      imgIndex = imgIndex === allimages.length - 1 ? 0 : imgIndex + 1;
    }, 500);
    return () => clearInterval(interval);
  });

  let dimensions = [
    {
      width: 150,
      height: 60,
      rounded: 50,
      rotate: 0,
    },
    {
      width: 200,
      height: 200,
      rounded: 20,
      rotate: 0,
    },
    {
      width: 200,
      height: 300,
      rounded: 40,
      rotate: -25,
    },
    {
      width: 250,
      height: 250,
      rounded: 60,
      rotate: 45,
    },
    {
      width: 200,
      height: 200,
      rounded: 20,
      rotate: 0,
    },
    {
      width: 60,
      height: 60,
      rounded: 50,
      rotate: 0,
    },
  ];
  let width = spring(dimensions[state].width, { stiffness: 0.1, damping: 0.8 });
  let height = spring(dimensions[state].height, {
    stiffness: 0.1,
    damping: 0.8,
  });
  let rounded = spring(dimensions[state].rounded, {
    stiffness: 0.1,
    damping: 0.6,
  });
  let rotate = spring(dimensions[state].rotate, {
    stiffness: 0.1,
    damping: 0.9,
  });

  onMount(() => {
    const interval = setInterval(() => {
      if (state === dimensions.length - 1) {
        state = 0;
      } else {
        state += 1;
      }
      width.set(dimensions[state].width);
      height.set(dimensions[state].height);
      rounded.set(dimensions[state].rounded);
      rotate.set(dimensions[state].rotate);
    }, 900);
    return () => clearInterval(interval);
  });
</script>

<!-- to check manually via incrementing the state  -->
<!-- <div class="absolute top-10 left-10">
  <Button
    on:click={() => {
      if (state === dimensions.length - 1) {
        state = 0;
      } else {
        state += 1;
      }
      width.set(dimensions[state].width);
      height.set(dimensions[state].height);
      rounded.set(dimensions[state].rounded);
      rotate.set(dimensions[state].rotate);
    }}>Update</Button
  >
</div> -->

<div class="flex justify-center items-center min-h-screen">
  <div class="text-3xl font-semibold">
    I love to
    <img
      src={allimages[imgIndex]}
      alt="doodle"
      class="inline-block object-cover {state === 2
        ? 'mx-8'
        : state === 3
          ? 'mx-8'
          : 'mx-2'}"
      style="border-radius: {$rounded}px; width:{$width}px; height:{$height}px; transform:rotate({$rotate}deg);"
    />
    in Svelte
  </div>
</div>
