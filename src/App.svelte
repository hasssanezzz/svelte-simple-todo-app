<script>
  import TodoList from "./components/TodoList.svelte"
  import AddTodo from "./components/AddTodo.svelte"
</script>

<div class="container">
  <h2>Craete a new one</h2>
  <AddTodo />

  <h2>My todos</h2>
  <TodoList />
</div>

<style>
  .container {
    padding: 20px;
    padding-top: 0;
  }
</style>
