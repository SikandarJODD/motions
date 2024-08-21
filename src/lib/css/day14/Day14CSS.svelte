<div class="wrapper">
  <h5>Passwords</h5>
  <p>
    Simple and secure password authentication, complete with breach detection
    and recovery options.
  </p>

  <div class="animation-wrapper">
    <svg
      width="317"
      height="214"
      viewBox="0 0 317 214"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
      class="svg-background transition"
    >
      <path
        d="M21.6502 2.38322L2.30334 22.0051C0.827423 23.502 0 25.5197 0 27.6219L0 214L317 214L317 27.6219C317 25.5197 316.173 23.502 314.697 22.0051L295.35 2.38322C293.846 0.858434 291.794 0 289.653 0L27.3468 0C25.2055 0 23.1536 0.858435 21.6502 2.38322Z"
        fill="#2B2B30"
        stroke="white"
        stroke-opacity="0.04"
      ></path>
    </svg>

    <div class="lock transition">
      <svg
        width="8"
        height="36"
        viewBox="0 0 8 36"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          fill="black"
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M3 0C1.34315 0 0 1.34315 0 3V19.5858C0 19.851 0.105357 20.1054 0.292893 20.2929L3.29289 23.2929C3.68342 23.6834 3.68342 24.3166 3.29289 24.7071L0.292893 27.7071C0.105357 27.8946 0 28.149 0 28.4142V33C0 34.6569 1.34315 36 3 36H5C6.65685 36 8 34.6569 8 33V16.4142C8 16.149 7.89464 15.8946 7.70711 15.7071L4.70711 12.7071C4.31658 12.3166 4.31658 11.6834 4.70711 11.2929L7.70711 8.29289C7.89464 8.10536 8 7.851 8 7.58579V3C8 1.34315 6.65685 0 5 0H3Z"
        ></path>
      </svg>

      <div class="shine"></div>
    </div>

    <div class="input transition">
      <div class="dot" style="--i: 1"></div>
      <div class="dot" style="--i: 2"></div>
      <div class="dot" style="--i: 3"></div>
      <div class="dot" style="--i: 4"></div>
      <div class="dot" style="--i: 5"></div>
      <div class="dot" style="--i: 6"></div>
      <div class="dot" style="--i: 7"></div>
      <div class="dot" style="--i: 8"></div>
      <div class="dot" style="--i: 9"></div>
      <div class="dot" style="--i: 10"></div>
    </div>
  </div>
</div>

<style>
  

  .wrapper {
    --duration: 400ms;
    --y: 40px;
    --primary: rgb(58 212 253);
    position: relative;
    width: 100%;
    height: 260px;
    max-width: 400px;
    background-color: rgb(33 33 38);
    border-radius: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: end;
    align-items: start;
    padding: 0 24px 24px;

  }

  .transition {
    transition: var(--duration);
  }

  .wrapper h5 {
    color: white;
  }

  .wrapper p {
    font-size: 0.8125rem;
    line-height: 1.25rem;
    margin-top: 0.5rem;
  }

  .animation-wrapper {
    position: absolute;
    height: 65%;
    top: 0;
    left: 0;
    right: 0;
    overflow: hidden;
    display: flex;
    justify-content: center;
  }

  .animation-wrapper::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 30%;
    background: linear-gradient(to bottom, transparent, rgb(33 33 38));
  }

  .animation-wrapper .svg-background {
    position: absolute;
    transform: translateY(100px);
  }

  .wrapper:hover .animation-wrapper svg {
    transform: translateY(calc(100px - var(--y)));
  }

  .animation-wrapper .lock {
    position: absolute;
    width: 64px;
    height: 64px;
    background-color: #2b2b30;
    box-shadow: 0 0 0 4px black;
    border-radius: 9999px;
    transform: translateY(70px);
    display: flex;
    justify-content: center;
    align-items: center;
    isolation: isolate;
    overflow: hidden;
  }

  .animation-wrapper .lock::after {
    content: "";
    position: absolute;
    inset: 0;
    background-image: repeating-radial-gradient(
      rgba(0, 0, 0, 0.2) 0.125rem,
      transparent 0.25rem
    );
    border-radius: 9999px;
    box-shadow: inset 0 1px 2px rgba(255, 255, 255, 0.1);
    z-index: -2;
  }

  .animation-wrapper .lock::before {
    content: "";
    position: absolute;
    inset: 16px;
    background-image: repeating-radial-gradient(
      rgba(0, 0, 0, 0.2) 0.125rem,
      transparent 0.25rem
    );
    border-radius: 9999px;
    box-shadow: inset 0 3px 1px rgba(0, 0, 0, 0.206);
    z-index: -2;
  }

  .animation-wrapper .lock svg {
    position: absolute;
    transition: var(--duration);
  }

  .animation-wrapper .lock .shine {
    width: 100%;
    height: 100%;
    background-image: linear-gradient(
      90deg,
      transparent,
      hsla(0, 0%, 100%, 0.5) 30%,
      #fff,
      hsla(0, 0%, 100%, 0.5) 70%,
      transparent
    );
    opacity: 0.1;
    transform: translateX(-125%) translateY(-75%) rotate(45deg) scaleY(1.2);
    transition: var(--duration);
  }

  .animation-wrapper .input {
    width: 224px;
    height: 28px;
    background-color: #2f3037;
    transform: translateY(150px);
    border-radius: 0.375rem;
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    gap: 0.4rem;
    padding-inline: 0.7rem;
  }

  .animation-wrapper .input .dot {
    width: 5px;
    height: 5px;
    background-color: var(--primary);
    border-radius: 1rem;
    opacity: 0;
    scale: 2;
    filter: blur(4px);
    box-shadow: 0 2px 1px rgb(0, 0, 0, 0.2);
    transition: var(--duration);
  }

  .wrapper:hover .animation-wrapper .lock {
    transform: translateY(calc(70px - var(--y)));
  }

  .wrapper:hover .animation-wrapper .lock svg {
    transform: translateY(calc(40px - var(--y))) rotate(90deg);
    transition: calc(100ms + var(--duration)) cubic-bezier(1, 0.005, 0, 0.985)
      700ms;
  }

  .wrapper:hover .animation-wrapper .lock .shine {
    transform: translateX(0%) translateY(0%) rotate(45deg) scaleY(1.2);
    transition: calc(100ms + var(--duration)) cubic-bezier(1, 0.005, 0, 0.985)
      700ms;
  }

  .wrapper:hover .animation-wrapper .input {
    transform: translateY(calc(160px - var(--y)));
  }

  .wrapper:hover .animation-wrapper .input {
    box-shadow: 0 0 0px 1px var(--primary);
  }
  .wrapper:hover .animation-wrapper .input .dot {
    opacity: 1;
    scale: 1;
    filter: blur(0px);
    transition-delay: calc(0.05s * var(--i));
  }
</style>
