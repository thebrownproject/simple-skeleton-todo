<script lang="ts">
  // Todo list class
  class Todo {
    id: number;
    completed: boolean = false;
    text: string;
    constructor(id: number, text: string) {
      this.id = id;
      this.text = text;
    }
  }
  let id = 0;

  let todoList = $state([
    new Todo(id++, "Learn Svelte"),
    new Todo(id++, "Learn SvelteKit"),
    new Todo(id++, "Learn TypeScript"),
  ]);

  // Function to add a new todo
  function addTodo(todoText: string) {
    const text = todoText;
    const newTodo = new Todo(id++, text);
    todoList.push(newTodo);
  }

  // Function to remove a todo
  function removeTodo(todoId: number) {
    todoList = todoList.filter((todo) => todo.id !== todoId);
  }

  // Function to toggle the completed state of a todo
  function toggleTodo(todoId: number) {
    const todo = todoList.find((todo) => todo.id === todoId);
    if (todo) {
      todo.completed = !todo.completed;
    }
  }

  // Function to update text of todo 
  function updateTodo(todoId: number, newText: string) {
    const todo = todoList.find ((todo) => todo.id === todoId);
    if (todo) {
        todo.text = newText;
    }


</script>

<h1>Welcome to SvelteKit</h1>
<p>
  Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the
  documentation
</p>
