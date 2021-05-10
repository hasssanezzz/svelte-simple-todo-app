<script>
  import { todos } from "../store"

  // the binded value
  let name = ""

  function handleSubmission(e) {
    e.preventDefault()

    let newTodo = {
      id: Date.now(),
      name,
      done: false,
    }

    todos.update((t) => {
      return [...t, newTodo]
    })

    name = ""
  }
</script>

<form on:submit={handleSubmission}>
  <input type="text" placeholder="Todo name..." bind:value={name} />

  <button>Add</button>
</form>
