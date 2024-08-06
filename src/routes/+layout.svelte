<script>
  import Footer from "$lib/dev/components/footer/Footer.svelte";
  import Navbar from "$lib/dev/components/navbars/Navbar.svelte";
  import "../app.css";
  import { ModeWatcher } from "mode-watcher";
</script>

<ModeWatcher />
<Navbar />
<slot></slot>
<!-- <Footer /> -->
