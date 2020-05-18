<script>
  import { onMount } from 'svelte';

  const TODO_API_URL = 'http://localhost:3000/api/v1'

  let promise = Promise.resolve([]);
  let todos = []
  let taskInput = ""
  let lastOrder = 0

  function addTask(event) {
    if (!event.key || event.key === 'Enter') {
      lastOrder++
      let newTask = { description: taskInput, order: lastOrder, status: 'todo' }
      todos = [...todos, newTask]
      saveTask(newTask)
      taskInput = ""
    }
  }

  async function saveTask(task) {
    const response = await self.fetch(`${TODO_API_URL}/tasks`, {
      method: 'POST',
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(task)
    })

    if (response.ok) {
      return response.json();
    } else {
      throw new Error(response);
    }
  }

	async function fetchTasks() {
		const response = await self.fetch(`${TODO_API_URL}/tasks`);

		if (response.ok) {
  		return response.json();
		} else {
			throw new Error(response);
		}
  }

  onMount(async () => {
    todos = await fetchTasks()
    if (todos.length > 0) {
      lastOrder = todos[todos.length - 1].order
    }
  })
</script>

<main>
  <ul>
    {#each todos as todo}
      <li>{todo.description}</li>
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
