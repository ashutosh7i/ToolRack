<script>
  import "../app.pcss";
  import "./styles.css";
  import Navbar from "../components/Navbar.svelte";
  import Footer from "../components/Footer.svelte";
  import Sidebar from "../components/Sidebar.svelte";
</script>

<div class="app">
  <Navbar />

  <main>
    <slot />
  </main>

  <Footer />
</div>
