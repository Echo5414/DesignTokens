
<script>
  import { createEventDispatcher } from 'svelte';

  export let variable;
  const dispatch = createEventDispatcher();

  function deleteVariable() {
    dispatch('delete');
  }
</script>

<div>
  <input type="text" bind:value={variable.name} placeholder="Variable Name" />

  {#if variable.type === 'color'}
    <input type="color" bind:value={variable.value} />
  {:else if variable.type === 'number'}
    <input type="number" bind:value={variable.value} />
  {:else if variable.type === 'string'}
    <input type="text" bind:value={variable.value} />
  {:else if variable.type === 'boolean'}
    <input type="checkbox" bind:checked={variable.value} />
  {/if}

  <button on:click={deleteVariable}>Delete Variable</button>
</div>

<style>
  /* Add some basic styling */
</style>
