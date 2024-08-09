<script>
  import { onMount } from "svelte";
  import DiscordCard from "./DiscordCard.svelte";
  import PeerSpace from "./PeerSpace.svelte";
  import Wrapper from "../Wrapper.svelte";
  import UrbanSitter from "./UrbanSitter.svelte";
  import Shippo from "./Shippo.svelte";

  let cards = [
    {
      id: 1,
      color: "#5865F2",
      text: "We decided to build the Verified Bot program on Stripe Identity for three reasons: the user experience was seamless, integration was easier since we’re already using Stripe for payments, and our users trusted Stripe to help keep their identity information safe and secure.",
      logo: DiscordCard,
    },
    {
      id: 2,
      color: "#E72A54",
      text: "We were able to easily update our existing Connect onboarding experience to collect additional verifications using Stripe Identity. This allows us to control payouts based on verification status to reduce fraud, while keeping our hosts on a single, consistent experience that’s powered by Stripe.",
      logo: PeerSpace,
    },
    {
      id: 3,
      color: "#8CB548",
      text: "Stripe Identity has been a game changer for us. We were able to quickly integrate it into our existing platform and it has helped us reduce fraud and improve our user experience. We’re excited to continue working with Stripe to build new features and products that help us grow our business.",
      logo: Shippo,
    },
    {
      id: 4,
      color: "#00bbcd",
      text: "Stripe Identity has been a game changer for us. We were able to quickly integrate it into our existing platform and it has helped us reduce fraud and improve our user experience. We’re excited to continue working with Stripe to build new features and products that help us grow our business.",
      logo: UrbanSitter,
    },
  ];
  let selectedCard = 0;
  let change = true;
  onMount(() => {
    let timeout = setTimeout(() => {
      change = true;
    }, 300);
    return () => clearTimeout(timeout);
  });
</script>

<Wrapper class="isolate px-8">
  <div
    class="relative isolate mx-auto flex min-h-96 w-full max-w-5xl items-center overflow-hidden rounded-xl bg-white py-12"
    style="
      box-shadow:0 50px 100px -20px rgba(50,50,93,0.25), 0 30px 60px -30px rgba(0,0,0,0.3);"
    style:--userLogoColor="white"
  >
    {#each cards as card (card)}
      <div
        class="grid w-full items-center gap-8 p-8 duration-700 ease-in-out md:grid-cols-2 md:gap-4"
        style="
          flex: 0 0 auto;
          transform: translateX(-{selectedCard * 100}%);
          opacity: {selectedCard === card.id - 1 ? 1 : 0};
        "
      >
        <div>
          <p
            class={`text-xl text-white before:absolute before:-translate-x-3 before:content-['_"'] after:content-['_"']`}
          >
            {card.text}
          </p>
        </div>
        <div class="flex items-center justify-center text-white">
          <div class="w-96">
            <svelte:component this={card.logo} />
          </div>
        </div>
      </div>
    {/each}
    <div
      class="absolute inset-0 -z-10 duration-1000"
      style=" background: {cards[selectedCard].color};"
    />
  </div>
  <div class="lg::gap-y-0 mt-12 grid grid-cols-2 gap-y-8 lg:grid-cols-4">
    {#each cards as card, index}
      <button
        class="w-full max-w-64 px-4 outline-none"
        on:click={() => {
          selectedCard = index;
          change = false;
        }}
        style:--userLogoColor={index === selectedCard ? "" : "#aab4c1"}
      >
        <svelte:component this={card.logo} />
      </button>
    {/each}
  </div>
  <!-- {/* Grid Lines */} -->
  <div
    class="absolute isolate -z-20 grid h-full w-full max-w-5xl grid-cols-2 overflow-hidden lg:grid-cols-4"
  >
    <div class="h-full w-px bg-[#aab4c1]/20"></div>
    <svg class="hidden h-full lg:block">
      <line
        x1="0"
        y1="0"
        x2="0"
        y2="100%"
        stroke-width={3}
        stroke-dasharray={8}
        class="stroke-[#aab4c1]/20"
      />
    </svg>
    <svg class="hidden h-full lg:block">
      <line
        x1="0"
        y1="0"
        x2="0"
        y2="100%"
        stroke-width={3}
        stroke-dasharray={8}
        class="stroke-[#aab4c1]/20"
      />
    </svg>
    <svg class="h-full">
      <line
        x1="0"
        y1="0"
        x2="0"
        y2="100%"
        stroke-width={3}
        stroke-dasharray={8}
        class="stroke-[#aab4c1]/20"
      />
    </svg>
    <div class="absolute right-0 top-0 h-full w-px bg-[#aab4c1]/20"></div>
  </div>
</Wrapper>
