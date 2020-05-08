<script>
  let todos = []
  let taskInput = ""

  function addTask(event) {
    if (!event.key || event.key === 'Enter') {
      todos = [...todos, taskInput]
      taskInput = ""
    }
  }
</script>

<main>
  <ul>
    {#each todos as todo}
      <li>{todo}</li>
    {/each}
  </ul>

  <div class="flex">
    <label>
      New Task:
      <input bind:value="{taskInput}" on:keydown={addTask} />
    </label>
    <button on:click={addTask}>Add Task</button>
  </div>
</main>

<style>
  ul {
    list-style-type: none;
  }

  .flex {
    display: flex;
    justify-content: center;
  }
</style>
