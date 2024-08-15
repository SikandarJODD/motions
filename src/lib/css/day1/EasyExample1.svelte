<div class="box" style="--i: 1;"></div>

<style>
  .box {
    width: 100px;
    height: 80px;
    margin: 40px;
    background-color: #3498db;
    animation: rotate-reverse 3s infinite;
  }


  @keyframes rotate-reverse {
    from {
      transform: rotate(calc(-60deg * var(--i)));
    }
    to {
      transform: rotate(calc(-360deg - 60deg * var(--i)));
    }
  }
</style>
