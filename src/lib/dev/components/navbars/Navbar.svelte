<script>
  import { slide } from "svelte/transition";
  import { Home, Sparkle, MousePointerClick, User } from "lucide-svelte";

  export let navs = [
    {
      name: "Home",
      href: "/",
      icon: Home,
    },
    {
      name: "Animations",
      href: "/animations",
      icon: Sparkle,
    },
    {
      name: "CSS",
      href: "/",
      icon: MousePointerClick,
    },
    {
      name: "About",
      href: "/",
      icon: User,
    },
  ];
  let isMobileMenuOpen = false;
</script>

<nav class="bg-background sticky top-0 backdrop-blur-md">
  <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
    <div class="relative flex h-16 items-center justify-between">
      <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
        <!-- Mobile menu button-->
        <button
          type="button"
          class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:text-white outline-none"
          aria-controls="mobile-menu"
          aria-expanded="false"
          on:click={() => {
            isMobileMenuOpen = !isMobileMenuOpen;
          }}
        >
          <span class="absolute -inset-0.5"></span>
          <span class="sr-only">Open main menu</span>
          <!-- Hamburger Icon -->
          <svg
            class="{isMobileMenuOpen ? 'hidden' : 'block'}  h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
            />
          </svg>
          <!-- X icon -->
          <svg
            class="{isMobileMenuOpen ? 'block' : 'hidden'} h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            aria-hidden="true"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        </button>
      </div>
      <div
        class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-center"
      >
        <div class="flex flex-shrink-0 items-center">
          <a
            href="/"
            class="border rounded-full h-8 w-8 flex justify-center items-center"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.4"
              stroke-linecap="round"
              stroke-linejoin="round"
              class="lucide lucide-slash -rotate-6"><path d="M22 2 2 22" /></svg
            >
          </a>
        </div>
        <div class="hidden sm:ml-6 sm:block">
          <div class="flex space-x-4">
            {#each navs as { name, href }}
              <a
                {href}
                class="rounded-md px-3 py-2 text-sm text-gray-300 hover:text-white"
                >{name}</a
              >
            {/each}
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Mobile menu, show/hide based on menu state. -->
  {#key isMobileMenuOpen}
    <div
      class="sm:hidden border-b {isMobileMenuOpen ? 'block' : 'hidden'}"
      id="mobile-menu"
      in:slide
    >
      <div class="space-y-1 px-2 pb-3 pt-2">
        {#each navs as { name, href, icon }}
          <a
            {href}
            class="flex items-center gap-1.5 rounded-md px-3 py-2 text-base font-medium text-gray-300 hover:text-white"
          >
            <svelte:component
              this={icon}
              strokeWidth={1.4}
              width={15}
              height={15}
            />
            {name}</a
          >
        {/each}
      </div>
    </div>
  {/key}
</nav>
