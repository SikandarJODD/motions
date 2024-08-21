<script lang="ts">
  import "./day7.css";
  let day7 = (node: Document) => {
    let textValue = "sikandar@bhidesvelte.com";

    let text = node.querySelector(".text");
    let wrapper = node.querySelector(".wrapper");
    let buttons = node.querySelectorAll("button");
    let border: HTMLElement = node.querySelector(".bordercode") || null;
    let borderTexts = node.querySelectorAll(".bordercode p");

    let [beforeAt, afterAt] = textValue.split("@");
    // console.log(beforeAt, afterAt, "@");
    let [before, after] = afterAt.split(".");
    // console.log(before, after, ".");

    if (text) {
      text.innerHTML = `<span class="user" data-user="${beforeAt}">${beforeAt}</span><span class="symbol" data-user="@">@</span><span class="address" data-user="${before}">${before}</span><span class="com" data-user=".${after}">.${after}</span>`;
    }
    buttons.forEach((button, index) => {
      button.addEventListener("mouseover", () => {
        let value = button.value;
        // console.log(value, "value");

        if (text) {
          let spans = text.querySelectorAll(`span`);

          spans.forEach((span) => span.classList.remove("active"));

          if (border) {
            // console.log(border, "border", index);
            border.classList.add("active");

            borderTexts[index].classList.add("active");

            if (value === "user") {
              let element = text.querySelector(`.${value}`);

              if (element) {
                element.classList.add("active");
                border.style.setProperty(
                  "--width",
                  `${element.getBoundingClientRect().width}px`
                );
                if (wrapper) {
                  border.style.setProperty(
                    "--left",
                    `${element.getBoundingClientRect().left - wrapper.getBoundingClientRect().left}px`
                  );
                }
              }
            } else if (value === "link") {
              const elements = [
                text.querySelector(".address"),
                text.querySelector(".com"),
              ];

              ElementsAddingClass(elements);
            } else if (value === "email") {
              const elements = [
                text.querySelector(".user"),
                text.querySelector(".symbol"),
                text.querySelector(".address"),
                text.querySelector(".com"),
              ];

              ElementsAddingClass(elements);
            } else if (value === "social") {
              let elements = [
                text.querySelector(".symbol"),
                text.querySelector(".address"),
              ];
              ElementsAddingClass(elements);
            }
          }
        }
      });
    });

    buttons.forEach((button, index) => {
      button.addEventListener("mouseleave", () => {
        if (text) {
          let spans = text.querySelectorAll(`span`);
          //  remove active class from all span
          spans.forEach((span) => span.classList.remove("active"));

          // remove active class from border
          border.classList.remove("active");

          // remove active class from borderTexts at specific index
          borderTexts[index].classList.remove("active");
          // if we don't remove the above class all the names will be active & overlap each other
        }
      });
    });

    function ElementsAddingClass(elements: Array<HTMLElement>) {
      elements.forEach((element) => element.classList.add("active"));
      // calculate the total width of the elements
      // example : symbol + address
      // @ + bhidesvelte -> for Instagram

      let totalWidth = elements.reduce(
        (acc, element) => acc + element.getBoundingClientRect().width,
        0
      );
      //   console.log(totalWidth, "totalWidth");

      border.style.setProperty("--width", `${totalWidth}px`);
      // This is use to shift the border to the left
      border.style.setProperty(
        "--left",
        `${elements[0].getBoundingClientRect().left - wrapper.getBoundingClientRect().left}px`
      );
    }
  };
</script>

<svelte:document use:day7 />
<div class="wrapper">
  <h2 class="text"></h2>

  <div class="buttons">
    <button class="user-button" value="user">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="22"
        height="22"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.6"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="fa-regular fa-user"
        ><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2" /><circle
          cx="12"
          cy="7"
          r="4"
        /></svg
      >
    </button>
    <button class="link-button" value="link">
      <!-- <i class="fa-solid fa-link"></i> -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="22"
        height="22"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.6"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="fa-solid fa-link"
        ><path
          d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"
        /><path
          d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"
        /></svg
      >
    </button>
    <button class="email-button" value="email">
      <!-- <i class="fa-regular fa-envelope"></i> -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="22"
        height="22"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.6"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="fa-regular fa-envelope"
        ><rect width="20" height="16" x="2" y="4" rx="2" /><path
          d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"
        /></svg
      >
    </button>
    <button class="social-button" value="social">
      <!-- <i class="fa-brands fa-instagram"></i> -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="22"
        height="22"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="1.6"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="fa-brands fa-instagram"
        ><rect width="20" height="20" x="2" y="2" rx="5" ry="5" /><path
          d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"
        /><line x1="17.5" x2="17.51" y1="6.5" y2="6.5" /></svg
      >
    </button>
  </div>

  <div class="bordercode">
    <p>name</p>
    <p>website</p>
    <p>email</p>
    <p>Instagram</p>
  </div>
</div>
