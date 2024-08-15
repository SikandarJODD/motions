<script>
  import Wrapper from "$lib/components/animations/Wrapper.svelte";
  import "./day1.css";

  //   Images
  import SvelteSvg from "$lib/imgs/svelte.svg";
  import SupabaseSvg from "$lib/imgs/supabase.svg";
  import OpenAISvg from "$lib/imgs/openai.svg";
</script>

<Wrapper class="px-8">
  <!-- Credits : Ali Samadi
         Twitter : @alisamadi__
         Post : https://twitter.com/alisamadi__/status/1814797512496324875
         Motive : I am trying to Learn CSS Animation from Ali Samadi Portfolio - 
         Thankyou for the inspiration Ali Samadi, You mean a lottt to me.
      -->
  <div
    class="relative flex h-[474px] w-full max-w-[960px] flex-col items-center justify-center border"
  >
    <!-- 4 Corner Small Circles -->
    <div
      class="pointer-events-none absolute left-0 top-0 h-5 w-5 -translate-x-1/2 -translate-y-1/2 rounded-full border bg-white shadow-[0_0_0_5px_white]"
    />
    <div
      class="pointer-events-none absolute right-0 top-0 h-5 w-5 -translate-y-1/2 translate-x-1/2 rounded-full border bg-white shadow-[0_0_0_5px_white]"
    />
    <div
      class="pointer-events-none absolute bottom-0 right-0 h-5 w-5 translate-x-1/2 translate-y-1/2 rounded-full border bg-white shadow-[0_0_0_5px_white]"
    />
    <div
      class="pointer-events-none absolute bottom-0 left-0 h-5 w-5 -translate-x-1/2 translate-y-1/2 rounded-full border bg-white shadow-[0_0_0_5px_white]"
    />

    <!-- Main Animation Content -->
    <div class="relative grid h-[278px] w-full grid-cols-4 items-center">
      <div class="aspect-square rounded-full border"></div>

      <!-- First Animation Content -->
      <!-- This Includes 6 divs with --i from 1 to 6 -->
      <div class="animate-wrapper relative aspect-square rounded-full border">
        <div id="social-media-wrapper" class="image" style:--i="1">
          <span>
            <img
              src="https://mailmeteor.com/logos/assets/PNG/Gmail_Logo_512px.png"
              alt="gmail_logo"
            />
          </span>
        </div>

        <div id="social-media-wrapper" style:--i="2">
          <span></span>
        </div>

        <div id="social-media-wrapper" style:--i="3" class="image">
          <span>
            <img
              src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Slack_icon_2019.svg/2048px-Slack_icon_2019.svg.png"
              alt="slack_icon"
            />
          </span>
        </div>

        <div id="social-media-wrapper" style:--i="4">
          <span></span>
        </div>

        <div id="social-media-wrapper" style:--i="5" class="image">
          <span>
            <img
              src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Instagram_logo_2016.svg/2048px-Instagram_logo_2016.svg.png"
              alt="instagram_logo"
            />
          </span>
        </div>

        <div id="social-media-wrapper" style:--i="6">
          <span></span>
        </div>
      </div>

      <!-- Second Animation Content  -->
      <div
        class="animate-wrapper relative animate-reverse aspect-square rounded-full border"
      >
        <div id="social-media-wrapper" class="image" style:--i="1">
          <span>
            <img
              src={SvelteSvg}
              alt="Svelte_Logo"
            />
          </span>
        </div>

        <div id="social-media-wrapper" style:--i="2">
          <span></span>
        </div>

        <div id="social-media-wrapper" class="image" style:--i="3">
          <span>
            <img
              src={SupabaseSvg}
              alt="Supabase_Logo"
            />
          </span>
        </div>

        <div id="social-media-wrapper" style:--i="4">
          <span></span>
        </div>

        <div id="social-media-wrapper" class="image" style:--i="5">
          <span>
            <img
              src={OpenAISvg}
              alt="Open_AI_Logo"
            />
          </span>
        </div>

        <div id="social-media-wrapper" style:--i="6">
          <span></span>
        </div>
      </div>

      <div class="aspect-square rounded-full border"></div>

      <!-- Logo -->
      <div
        class="absolute left-1/2 top-1/2 grid h-[104px] w-[104px] -translate-x-1/2 -translate-y-1/2 grid-cols-5 place-content-center place-items-center gap-y-1 rounded-full bg-white/80 px-7 backdrop-blur-sm"
        style="box-shadow:0 0 0 1px #0e3f7e0a, 0 1px 1px -.5px #2a33450a, 0 3px 3px -1.5px #2a33460a, 0 6px 6px -3px #2a33460a, 0 12px 12px -6px #0e3f7e0a, 0 24px 24px -12px #0e3f7e0a ;"
      >
        <div
          class="dot-animation col-span-5 h-[6px] w-[6px] rounded-full bg-black"
          style:--i="4"
        />
        <div class="dot-animation h-[6px] w-[6px] rounded-full" style:--i="3" />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="3"
        />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="3"
        />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="3"
        />
        <div class="dot-animation h-[6px] w-[6px] rounded-full" style:--i="3" />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="2"
        />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="2"
        />
        <div class="dot-animation h-[6px] w-[6px] rounded-full" style:--i="2" />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="2"
        />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="2"
        />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="1"
        />
        <div
          class="dot-animation col-span-3 h-[6px] w-[6px] rounded-full"
          style:--i="1"
        />
        <div
          class="dot-animation h-[6px] w-[6px] rounded-full bg-black"
          style:--i="1"
        />
      </div>

      <!-- Gradient Background -->
      <div
        class="absolute left-0 top-0 h-full w-1/4 bg-gradient-to-r from-white to-transparent"
      ></div>
      <div
        class="absolute right-0 top-0 h-full w-1/4 bg-gradient-to-l from-white to-transparent"
      ></div>
    </div>

    <!-- Text -->
    <div class="mt-12 text-center">
      <h3 class="text-[20px]">24/7 DevOps Support</h3>
      <p class="mt-4 max-w-[472px] text-[#020B20BA]">
        We&apos;re here to help you with everything from cost management to
        architecture, so you&apos;re never left stranded.
      </p>
    </div>
  </div>
</Wrapper>
