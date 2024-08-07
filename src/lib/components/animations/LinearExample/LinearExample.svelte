<script lang="ts">
  import { MotionConfig } from "svelte-motion";
  import EachCard from "./EachCard.svelte";
  interface InitialValuesTypes {
    id: number;
    img: string;
    title: string;
    description: string;
  }
  let initialValues: InitialValuesTypes[] = [
    {
      id: 1,
      img: "https://linear.app/cdn-cgi/imagedelivery/fO02fVwohEs9s9UHFwon6A/fc435ee2-fabf-4f10-5a37-d89874f4bf00/f=auto,dpr=2,q=95,fit=scale-down,metadata=none",
      title: "Purpose-built for product development",
      description:
        "Purpose-built for product development Linear was developed with a specific purpose: to empower product teams to do their best work. Every aspect is intentionally designed to help teams focus on what they do best: Planning, building, and shipping great products. Because of its fit-to-purpose design, Linear is incredibly easy to use, but grows more powerful as you scale. It’s opinionated where it needs to be, but provides enough flexibility to adapt to your team’s unique way of working. We believe that this approach creates a better way to build products. And more than 10,000 product teams around the globe – from early-stage startups to public companies – agree.",
    },
    {
      id: 2,
      img: "https://linear.app/cdn-cgi/imagedelivery/fO02fVwohEs9s9UHFwon6A/0e6d3edd-cd37-4bf8-c1bf-b93960169400/f=auto,dpr=2,q=95,fit=scale-down,metadata=none",
      title: "Designed to move fast",
      description:
        "Purpose-built for product development Linear was developed with a specific purpose: to empower product teams to do their best work. Every aspect is intentionally designed to help teams focus on what they do best: Planning, building, and shipping great products. Because of its fit-to-purpose design, Linear is incredibly easy to use, but grows more powerful as you scale. It’s opinionated where it needs to be, but provides enough flexibility to adapt to your team’s unique way of working. We believe that this approach creates a better way to build products. And more than 10,000 product teams around the globe – from early-stage startups to public companies – agree.",
    },
    {
      id: 3,
      img: "https://linear.app/cdn-cgi/imagedelivery/fO02fVwohEs9s9UHFwon6A/99eeb9b8-3d99-4191-0081-9f302d26f400/f=auto,dpr=2,q=95,fit=scale-down,metadata=none",
      title: "Crafted to perfection",
      description:
        "Purpose-built for product development Linear was developed with a specific purpose: to empower product teams to do their best work. Every aspect is intentionally designed to help teams focus on what they do best: Planning, building, and shipping great products. Because of its fit-to-purpose design, Linear is incredibly easy to use, but grows more powerful as you scale. It’s opinionated where it needs to be, but provides enough flexibility to adapt to your team’s unique way of working. We believe that this approach creates a better way to build products. And more than 10,000 product teams around the globe – from early-stage startups to public companies – agree.",
    },
  ];
</script>

<div
  style="background:linear-gradient(180deg,transparent,rgba(97,106,115,.12) 40%,rgba(97,106,115,.12) 60%,rgba(97,106,115,0))"
  class="flex min-h-dvh w-full flex-col items-center justify-center"
>
  <header
    class="mx-auto grid w-full md:max-w-5xl grid-cols-1 md:grid-cols-2 items-center p-2 md:p-0"
  >
    <h1 class="text-3xl md:text-[56px] font-medium leading-[1.1em]">
      Made for modern product teams
    </h1>
    <p class="mx-auto w-full md:max-w-[400px] text-[17px] text-[#969799]">
      Linear is shaped by the practices and principles that distinguish
      world-class product teams from the rest: relentless focus, fast execution,
      and a commitment to the quality of craft.
    </p>
  </header>
  <div class="mx-auto my-8 flex w-full max-w-5xl flex-wrap gap-2 p-4 lg:p-0">
    <MotionConfig transition={{ duration: 0.7, type: "spring", bounce: 0 }}>
      {#each initialValues as item}
        <EachCard value={item} />
      {/each}
    </MotionConfig>
  </div>
</div>
