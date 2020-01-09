<script>
  import { fade, fly } from "svelte/transition";

  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function remove() {
    dispatch("remove", { id });
  }

  function toggleStatus() {
    let newStatus = !complete;
    dispatch("toggle", {
      id,
      newStatus
    });
  }

  export let id;
  export let text;
  export let complete;
</script>

<style>
  .is-complete {
    text-decoration: line-through;
    color: rgb(189, 189, 189);
  }

  span {
    margin-right: auto;
  }


</style>

<div class="pl-2 pt-2 pb-2 flex mb-4" in:fly={{ x: 900, duration: 500 }} out:fade>

  {#if complete}
    <span class="is-complete cursor-pointer" on:click={toggleStatus}>{text}</span>
    <button class="btn" on:click={toggleStatus}>✔️</button>
  {:else}
    <span class=" cursor-pointer" on:click={toggleStatus}>{text}</span>
    <button class="btn" on:click={toggleStatus}>❌</button>
  {/if}

  <button class="btn" on:click={remove}>🗑️</button>

</div>
