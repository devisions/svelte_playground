<script>
  import ItemInput from "./ItemInput.svelte";
  import { blurOnKey } from "./util";
  import { createEventDispatcher } from "svelte";

  export let item;
  export let categoryId; // The category it belongs to.
  export let dnd; // An object that has `drag` and `drop` methods.

  const dispatch = createEventDispatcher();

  let editing = false;
</script>

<style>
  button {
    background-color: transparent;
    border: none;
  }

  input[type="checkbox"] {
    --size: 24px;
    height: var(--size);
    width: var(--size);
  }

  li {
    display: flex;
    align-items: center;
  }

  .packed-true {
    color: gray;
    text-decoration: line-through;
  }

  span {
    margin: 0 10px;
  }
</style>

<!-- the UI -->

<li>
  <input type="checkbox" bind:checked={item.packed} />
  {#if editing}
    <ItemInput
      bind:value={item.name}
      on:blur={() => (editing = false)}
      on:keydown={blurOnKey} />
  {:else}
    <span
      class="packed-{item.packed}"
      on:click={() => (editing = true)}
      draggable="true"
      on:dragstart={event => dnd.drag(event, categoryId, item.id)}>
      {item.name}
    </span>
  {/if}
  <button class="icon" on:click={() => dispatch('deleteItem')}>
    &#x1F5D1;
  </button>
</li>
