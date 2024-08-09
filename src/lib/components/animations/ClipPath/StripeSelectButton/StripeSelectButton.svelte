<script lang="ts">
  import { cn } from "$lib/utils";
  import { onMount } from "svelte";
  import Wrapper from "../../Wrapper.svelte";

  let initialValues = [
    {
      id: 1,
      url: "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f4/BMW_logo_%28gray%29.svg/1200px-BMW_logo_%28gray%29.svg.png?20210211152514",
      color: "#2E409E", // BMW's primary color is black
    },
    {
      id: 2,
      url: "https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/Amazon_logo.svg/1206px-Amazon_logo.svg.png?20220213013322",
      color: "#FF9900", // Amazon's primary color is orange
    },
    {
      id: 3,
      url: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Maersk_Group_Logo.svg/270px-Maersk_Group_Logo.svg.png?20200710145134",
      color: "#009FDA", // Maersk's primary color is blue
    },
    {
      id: 4,
      url: "https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Twilio-logo-red.svg/2560px-Twilio-logo-red.svg.png",
      color: "#F22F46", // Twilio's primary color is red
    },
  ];
  let selectedImg = 1;
  let calculateClipPath = (selectedImg: number) => {
    const positions = ["0%", "25%", "50%", "75%"];
    return `inset(0px ${positions[4 - selectedImg]} 0px ${positions[selectedImg - 1]})`;
  };
</script>

<Wrapper>
  <div class="relative mx-auto grid w-full max-w-5xl grid-cols-4">
    {#each initialValues as value}
      <button
        class={cn(
          "flex h-32 grow items-center justify-center outline-none delay-300",
          value.id === selectedImg ? "" : "grayscale"
        )}
        on:click={() => (selectedImg = value.id)}
      >
        <img
          src={value.url}
          alt="code"
          class={value.id === 1 ? "h-10" : "h-8"}
        />
      </button>
    {/each}

    <div
      class="pointer-events-none absolute inset-0 grid grid-cols-4 duration-1000"
      style="
      transition-timing-function: cubic-bezier(0.4,0,0.2,1);
        clip-path: {calculateClipPath(selectedImg)};
      "
    >
      {#each initialValues as value}
        <div
          class="h-px w-full  "
          style="background: {value.color};"
        ></div>
      {/each}
    </div>
  </div>
</Wrapper>
