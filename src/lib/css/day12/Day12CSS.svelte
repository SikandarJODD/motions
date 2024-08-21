<script lang="ts">
  let words = ["Svelte is Fun", "Svelte is Fun"];
  //   let textAnimation = (node: Document) => {
  //     let texts = node.querySelectorAll(".textcode");
  //     texts.forEach((text, index) => {
  //       let letters = words[1].split("");
  //       letters.forEach((letter) => {
  //         let span = document.createElement("span");
  //         if (letter === " ") {
  //           letter = "\u00A0";
  //         }
  //         span.innerHTML = letter;
  //         text.appendChild(span);
  //       });
  //     });
  //   };
</script>

<!-- <svelte:document use:textAnimation /> -->

<div class="wrapper">
  <h1 class="text name">
    {#each words[0].split("") as item}
      {#if item === " "}
        <span> &nbsp; </span>
      {:else}
        <span>{item}</span>
      {/if}
    {/each}
  </h1>
</div>

<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
  }

  h1 {
    font-weight: 500;
    font-size: 1.2rem;
    text-transform: uppercase;
    transition: 600ms;
  }

  .wrapper:hover h1:not(:hover) {
    opacity: 0.2;
  }

  :global(span) {
    display: inline-block;
    transition: 400ms cubic-bezier(0.65, 0.005, 0.21, 1.65);
  }

  :global(.name:hover span:nth-child(1)) {
    transform: translate(10%, 10%) rotate(10deg);
    transition-duration: 1000ms;
  }

  :global(.name:hover span:nth-child(2)) {
    transform: translate(-10%, -20%) rotate(-10deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(3)) {
    transform: translate(-10%, -50%) rotate(10deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(4)) {
    transform: translate(10%, -60%) rotate(10deg);
    transition-duration: 1000ms;
  }

  :global(.name:hover span:nth-child(5)) {
    transform: translate(0%, -40%) rotate(10deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(6)) {
    transform: translate(5%, -20%) rotate(40deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(7)) {
    transform: translate(10%, 40%) rotate(20deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(8)) {
    transform: translate(-30%, 10%) rotate(30deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(9)) {
    transform: translate(-30%, 40%) rotate(30deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(10)) {
    transform: translate(0%, 50%) rotate(15deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(11)) {
    transform: translate(-80%, 80%) rotate(10deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(12)) {
    transform: translate(-65%, 100%) rotate(20deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(13)) {
    transform: translate(-50%, 100%) rotate(30deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(14)) {
    transform: translate(20%, 40%) rotate(10deg);
    transition-duration: 1000ms;
  }
  :global(.name:hover span:nth-child(15)) {
    transform: translate(0%, -40%) rotate(-10deg);
    transition-duration: 1000ms;
  }
</style>
