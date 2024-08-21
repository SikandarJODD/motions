<script lang="ts">
  let hoverFollow = (node: HTMLElement) => {
    node.addEventListener("mousemove", (event) => {
      let centerX = node.offsetWidth / 2;
      let centerY = node.offsetHeight / 2;

      let offsetX = event.offsetX - centerX;
      let offsetY = event.offsetY - centerY;

      node.style.setProperty("--x", `${offsetX}px`);
      node.style.setProperty("--y", `${offsetY}px`);
    });
  };
</script>

<div use:hoverFollow class="hover-box"></div>

<style>
  .hover-box {
    display: grid;
    width: min(600px, 70%);
    margin: auto;
    aspect-ratio: 1;
    border: 1px solid hsl(0, 0%, 80%);
    border-radius: 0.5rem;
    box-shadow:
      0 0 0.2rem hsl(0, 0%, 42%),
      inset 0 0 0.2rem hsl(180, 1%, 37%);
    overflow: hidden;
  }

  .hover-box::before {
    content: "";
    display: block;
    width: clamp(10px, 10%, 30px);
    aspect-ratio: 1;
    margin: auto;
    border-radius: 50%;
    border: 1px solid hsl(0, 0%, 80%);
    background: hsl(0, 1%, 86%);
  }

  .hover-box:hover::before {
    animation: enter 500ms forwards;
  }
  .hover-box::before {
    animation: exit 500ms forwards;
  }

  /* Enter Animatin  */
  @keyframes enter {
    from {
      translate: 0 0;
    }
    to {
      translate: var(--x) var(--y);
    }
  }
  /* Exit Animation */
  @keyframes exit {
    from {
      translate: var(--x) var(--y);
    }
    to {
      translate: 0 0;
    }
  }
</style>
