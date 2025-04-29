<script lang="ts">
  // Todo list class
  class Todo {
    id: number;
    completed: boolean = $state(false);
    text: string = $state("");
    constructor(id: number, text: string) {
      this.id = id;
      this.text = text;
    }
  }
  let id = 0;
  let todoText = $state("");

  let todoList = $state([
    new Todo(id++, "Learn Svelte"),
    new Todo(id++, "Learn SvelteKit"),
    new Todo(id++, "Learn TypeScript"),
  ]);

  // Function to add a new todo
  function addTodo(todoText: string) {
    const newTodo = new Todo(id++, todoText);
    todoList.push(newTodo);
  }

  // Function to remove a todo
  function removeTodo(todoId: number) {
    todoList = todoList.filter((todo) => todo.id !== todoId);
  }

  // Function to update text of todo
  function updateTodo(todoId: number, newText: string) {
    const todo = todoList.find((todo) => todo.id === todoId);
    if (todo) {
      todo.text = newText;
    }
  }
</script>

<h1>Welcome to To-Do App</h1>
<h2>Todo List</h2>
<input
  type="text"
  bind:value={todoText}
  placeholder="Enter a new todo"
  onkeydown={(e) => {
    if (e.key === "Enter" && todoText) {
      addTodo(todoText);
      todoText = "";
    }
  }}
/>
<ul>
  {#each todoList as todo}
    <li>
      <input type="checkbox" bind:checked={todo.completed} />
      {todo.text}
      <button onclick={() => removeTodo(todo.id)}>Remove</button>
      <button
        onclick={() => {
          const newText = prompt("Update todo text", todo.text);
          updateTodo(todo.id, newText || todo.text);
        }}>Rename</button
      >
    </li>
  {/each}
</ul>
