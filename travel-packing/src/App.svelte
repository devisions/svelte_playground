<script>
  import page from "page";
  import Checklist from "./Checklist.svelte";
  import Login from "./Login.svelte";
  import NotFound from "./NotFound.svelte";

  let targetPage = Login;

  page.redirect("/", "/login");

  page("/login", () => (targetPage = Login));
  page("/checklist", () => (targetPage = Checklist));
  page("*", () => (targetPage = NotFound));

  page.start();
</script>

<style>
  :global(body) {
    background-color: cornflowerblue;
  }

  .hero {
    --height: 7rem;

    background-color: orange;
    color: white;
    font-size: 4rem;
    height: var(--height);
    line-height: var(--height);
    margin: 0 0 3rem 0;
    text-align: center;
    vertical-align: middle;
    width: 100vw;
  }

  main {
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }
</style>

<main>

  <h1 class="hero">Travel Packing Checklist</h1>

  <svelte:component
    this={targetPage}
    on:login={() => page.show('/checklist')}
    on:logout={() => page.show('/login')} />

</main>
