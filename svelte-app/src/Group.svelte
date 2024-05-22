
<script>
  import { createEventDispatcher } from 'svelte';
  import Variable from './Variable.svelte';

  export let group;
  const dispatch = createEventDispatcher();

  function addVariable(type) {
    group.variables = [...group.variables, { type, name: '', value: '' }];
  }

  function deleteVariable(index) {
    group.variables = group.variables.filter((_, i) => i !== index);
  }

  function deleteGroup() {
    dispatch('delete');
  }
</script>

<div>
  <input type="text" bind:value={group.name} placeholder="Group Name" />
  <button on:click={() => addVariable('color')}>Add Color</button>
  <button on:click={() => addVariable('number')}>Add Number</button>
  <button on:click={() => addVariable('string')}>Add String</button>
  <button on:click={() => addVariable('boolean')}>Add Boolean</button>
  <button on:click={deleteGroup}>Delete Group</button>

  {#each group.variables as variable, index}
    <Variable {variable} on:delete={() => deleteVariable(index)} />
  {/each}
</div>

<style>
  /* Add some basic styling */
</style>
