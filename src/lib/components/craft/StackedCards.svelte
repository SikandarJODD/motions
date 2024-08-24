<script>
  import SvelteLogo from "$lib/imgs/svelte.svg";
  import SupabaseLogo from "$lib/imgs/supabase.svg";
  import ClaudeLogo from "$lib/imgs/claude-ai.svg";
  import SpotifyLogo from "$lib/imgs/spotify.svg";
  import Wrapper from "../animations/Wrapper.svelte";
  let cards = [
    {
      id: 1,
      title: "Claud AI",
      company: "Linear, Inc.",
      desc: "Claude is trained to have natural, text-based conversations, and it excels in tasks like summarization, editing, Q&A, decision-making, code-writing, and more..",
      logo: ClaudeLogo,
      date: "March 2023", // initial release date from Wikipedia
    },
    {
      id: 2,
      title: "Spotify",
      company: "Spotify AB",
      desc: "Spotify is a Swedish audio streaming and media services provider, launched in October 2008.",
      logo: SpotifyLogo,
      date: "October 2008",
    },
    {
      id: 3,
      title: "Supabase",
      company: "Supabase ",
      desc: "Supabase is an open-source Firebase alternative that provides a full PostgreSQL database.",
      logo: SupabaseLogo,
      date: "January 2020",
    },
    {
      id: 4,
      title: "Svelte",
      company: "Rich Harris", // Creator of Svelte
      desc: "Svelte is a free and open-source front end JavaScript framework that is written in TypeScript.",
      logo: SvelteLogo,
      date: "November 2016",
    },
  ];
</script>

<Wrapper class="min-h-screen">
  <div class="flex justify-center items-center flex-col">
    {#each cards as { id, title, company, desc, logo, date }}
      <div class="p-3 m-2 w-2/3 bg-white rounded-xl border flex gap-4">
        <div class="flex items-center justify-between">
          <div class="size-[70px] bg-neutral-50 border rounded-[14px] p-1.5">
            <img
              src={logo}
              alt={title}
              class="w-full h-full"
              style="border-radius: 14px; transform: none; transform-origin: 50% 50% 0px;"
            />
            <!-- <img src={logo} alt={title} class="w-full h-full" /> -->
          </div>
        </div>
        <div class='w-full'>
          <div class="flex gap-4 items-center">
            <div class="flex gap-1 items-center">
              <h2 class="text-lg sm:text-xl font-semibold">{title}</h2>
              <span class="w-1 h-1 rounded-full bg-slate-800 line-clamp-1"
              ></span>
            </div>
            <p class="text-sm text-gray-500 line-clamp-1">{company}</p>
          </div>
          <p class=" text-gray-600">{desc}</p>
          <p class="mt-2 text-xs text-gray-400 w-full text-right pr-4">{date}</p>
        </div>
      </div>
    {/each}
  </div>
</Wrapper>
