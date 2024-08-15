<script>
  import "./day9.css";
  let code = (node) => {
    const wrapper = document.querySelector(".wrapper");
    const dotsAnimation = document.querySelector(".dots-animation");

    let counter = 1;

    function addingDelay(index) {
      if (index % 22 === 0) {
        counter = 1;
      }

      return counter++;
    }
    Array.from({ length: 110 }).map((_, index) => {
      let divElement = document.createElement("div");
      divElement.setAttribute("data-index", `${index + 1}`);
      divElement.setAttribute("data-light", "true");
      divElement.setAttribute("data-state", "off");
      divElement.style.setProperty("--i", `${addingDelay(index)}`);

      dotsAnimation.append(divElement);
    });

    let activeIndex = [
      1, 2, 3, 5, 7, 9, 10, 11, 13, 16, 17, 18, 20, 21, 22, 23, 27, 29, 31, 35,
      39, 42, 45, 46, 47, 49, 51, 53, 54, 57, 61, 64, 65, 69, 71, 73, 75, 79,
      83, 86, 89, 90, 91, 94, 97, 98, 99, 101, 102, 103, 105, 108, 109, 110,55,66
    ];

    if (wrapper) {
      wrapper.addEventListener("mouseover", () => {
        let eachDots = document.querySelectorAll("[data-light]");

        activeIndex.map((value) => {
          eachDots[value - 1].setAttribute("data-state", "high");
        });
      });
    }

    wrapper.addEventListener("mouseleave", () => {
      const eachDots = document.querySelectorAll("[data-light]");

      eachDots.forEach((dot) => {
        dot.setAttribute("data-state", "off");
      });
    });
  };
</script>

<svelte:document use:code />

<div class="wrapper">
  <div class="dots-animation"></div>
  <div>
    <h2 class='tracking-1' >Svelte 5</h2>
    <p>Svelte is a new way to build web applications.</p>
  </div>
</div>
