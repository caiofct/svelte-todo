<script>
  let todos = ['Task 1', 'Task 2', 'Task 3']

  function addTask() {
    todos = [...todos, 'New Task']
  }
</script>

<main>
  <ul>
    {#each todos as todo}
      <li>{todo}</li>
    {/each}
  </ul>

  <button on:click={addTask}>Add Task</button>
</main>

<style>
  ul {
    list-style-type: none;
  }
</style>
