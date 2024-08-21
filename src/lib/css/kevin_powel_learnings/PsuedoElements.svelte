<script>
</script>

<div>
  <p>Coding is fun</p>
</div>

<style>
  p::before {
    content: "";
    display: block;
    width: 0px;
    height: 1px;
    background-color: white;
  }

  p::after {
    content: "";
    display: block;
    width: 0px;
    height: 1px;
    background-color: white;
  }
  p:hover::after {
    width: 100%;
    transition: width 0.5s 0.5s;
  }
  p:hover::before {
    width: 100%;
    transition: width 0.5s;
  }
</style>
