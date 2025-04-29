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

<div class="container mx-auto max-w-3xl p-4">
  <ul>
    {#each todoList as todo}
      <li class="mb-2">
        <div
          class="card p-4 preset-filled-surface-100-900 flex items-center justify-between gap-4"
        >
          <div class="flex items-center gap-2">
            <input
              type="checkbox"
              class="checkbox rounded w-5 h-5 accent-primary-500 cursor-pointer"
              bind:checked={todo.completed}
            />
            <span
              style:text-decoration={todo.completed ? "line-through" : "none"}
            >
              {todo.text}
            </span>
          </div>
          <div class="flex gap-2">
            <button
              class="btn preset-tonal-error text-sm"
              onclick={() => removeTodo(todo.id)}
            >
              Remove
            </button>
            <button
              class="btn preset-tonal-surface text-sm"
              onclick={() => {
                const newText = prompt("Update todo text", todo.text);
                if (newText !== null) {
                  updateTodo(todo.id, newText || todo.text);
                }
              }}
            >
              Rename
            </button>
          </div>
        </div>
      </li>
    {/each}
  </ul>

  <input
    type="text"
    class="input mb-6"
    bind:value={todoText}
    placeholder="Enter a new todo"
    onkeydown={(e) => {
      if (e.key === "Enter" && todoText) {
        addTodo(todoText);
        todoText = "";
      }
    }}
  />
</div>
