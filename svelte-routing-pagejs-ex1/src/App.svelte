<script>
  import page from "page";
  import { cartStore } from "./stores";

  import Cart from "./Cart.svelte";
  import NotFound from "./NotFound.svelte";
  import Ship from "./Ship.svelte";
  import Shop from "./Shop.svelte";

  let component;

  page.redirect("/", "/shop");
  page("/cart", () => (component = Cart));
  page("/ship", () => (component = Ship));
  page("/shop", () => (component = Shop));

  page("*", () => (component = NotFound));

  page.start();
</script>

<style>
  :root {
    --space: 0.5rem;
  }

  a {
    background-color: white;
    border-radius: var(--space);
    margin-right: var(--space);
    padding: var(--space);
    text-decoration: none;
  }

  a.active {
    background-color: yellow;
  }

  .icon {
    padding-bottom: 6px;
    padding-top: 6px;
  }

  main {
    padding: var(--space);
  }

  nav {
    display: flex;
    align-items: center;
    background-color: cornflowerblue;
    padding: var(--space);
  }
</style>

<nav>
  <a href="/shop" class:active={component === Shop}>Shop</a>
  <a class="icon" href="/cart" class:active={component === Cart}>
    &#x1F6D2; {$cartStore.length}
  </a>
  <a href="/ship" class:active={component === Ship}>Ship</a>
</nav>

<main>
  <svelte:component this={component} />
</main>
