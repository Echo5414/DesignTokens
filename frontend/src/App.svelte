
<script>
  import { onMount } from 'svelte';
  import Group from './Group.svelte';

  let groups = [];

  // Load groups from local storage on mount
  onMount(() => {
    const storedGroups = localStorage.getItem('groups');
    if (storedGroups) {
      groups = JSON.parse(storedGroups);
    }
  });

  // Save groups to local storage whenever they change
  $: localStorage.setItem('groups', JSON.stringify(groups));

  function addGroup() {
    groups = [...groups, { name: 'New Group', variables: [] }];
  }
</script>

<main>
  <h1>Design Tokens</h1>
  <button on:click={addGroup}>Create Group</button>
  {#each groups as group, index}
    <Group {group} on:delete={() => groups = groups.filter((_, i) => i !== index)} />
  {/each}
</main>

<style>
  /* Add some basic styling */
</style>
