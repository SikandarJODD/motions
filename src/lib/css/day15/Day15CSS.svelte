<div class="wrapper">
  <div class="svg">
    <div class="badge">Invite this person</div>
    <svg viewBox="0 0 288 256" fill="none" aria-hidden="true" class="">
      <path
        d="M4 0v112c0 8.837 7.163 16 16 16h248c8.837 0 16 7.163 16 16v112"
        stroke="currentColor"
      ></path>
      <path
        d="M4 0v112c0 8.837 7.163 16 16 16h248c8.837 0 16 7.163 16 16v112"
        stroke="url(#line-gradient)"
      ></path>
      <defs>
        <linearGradient id="line-gradient" x1="0%" x2="0%" y1="0%" y2="0%">
          <stop stop-color="white" stop-opacity="0"></stop>
          <stop stop-color="black" offset="60%"></stop>
          <stop stop-color="black" offset="100%" stop-opacity="0"></stop>

          <animate
            attributeName="y1"
            values="0%; 120%"
            dur="2s"
            repeatCount="indefinite"
          />
          <animate
            attributeName="y2"
            values="-20%; 100%"
            dur="2s"
            repeatCount="indefinite"
          />

          <animate
            attributeName="x1"
            values="-20%; 120%"
            dur="2s"
            repeatCount="indefinite"
          />
          <animate
            attributeName="x2"
            values="-40%; 100%"
            dur="2s"
            repeatCount="indefinite"
          />
        </linearGradient>
      </defs>
    </svg>
  </div>

  <div>
    <h3>Day 15: Mastering CSS Animation</h3>
    <p>Thanks god, I am feeling better when working with CSS Animation.</p>
  </div>
</div>

<style>
  .wrapper {
    position: relative;
    width: 376px;
    height: 250px;
    box-shadow:
      1px 1px rgba(0, 0, 0, 0.05),
      0 4px 6px rgba(34, 42, 53, 0.04),
      0 24px 68px rgba(47, 48, 55, 0.05),
      0 2px 3px rgba(0, 0, 0, 0.04);
    border-radius: 1rem;
    display: flex;
    align-items: end;
    padding: 24px;
  }

  .wrapper .svg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: rgba(19, 19, 22, 0.1);
  }

  .wrapper .svg::after {
    content: "";
    position: absolute;
    inset: 0;
    background: linear-gradient(to bottom, transparent 50%, white);
  }

  .wrapper .svg .badge {
    position: relative;
    background-color: rgb(47 48 55);
    color: white;
    height: 28px;
    font-size: 0.6875rem;
    border-radius: 1rem;
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-inline: 1rem;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    overflow: hidden;
  }

  .wrapper .svg .badge::after {
    content: "";
    position: absolute;
    inset: 0;
    background: linear-gradient(
      to right,
      rgba(255, 255, 255, 0) 50%,
      rgba(255, 255, 255, 0.1),
      rgba(255, 255, 255, 0)
    );
    transform: translateX(-100%);
    animation: shine-animate 2s infinite;
  }

  @keyframes shine-animate {
    0%,
    35% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(100%);
    }
  }

  .wrapper .svg svg {
    width: 200px;
  }

  .wrapper {
    font-size: 0.8125rem;
  }

  .wrapper p {
    color: rgb(94 95 110);
    margin-top: 8px;
    line-height: 1.5;
  }
</style>
