<script>
  import { todos } from "../store"

  // component props
  export let todoName
  export let done
  export let index

  // defines if the todo is being edited
  let editable = false

  // defines if the user confirmes that he want to delete the todo
  let confirmed = false

  // when the user make a todo done
  function handleChange(e) {
    let checked = e.target.checked
    todos.update((t) => {
      let clone = t
      clone[index].done = checked
      return clone
    })
  }

  // when the user clicks the delete button
  function handleDelete() {

    if (confirmed) {
      todos.update((t) => {
        let clone = t
        clone.splice(index, 1)
        return clone
      })

      confirmed = false

    } else {
      confirmed = true
    }
  }

  // when the user submit after editing the todo's name
  function handleSubmission(e) {
    e.preventDefault()
    todos.update((t) => {
      let clone = t
      clone[index].name = todoName
      return clone
    })
    handleEditClick()
  }

  // toggle the "editable" variable
  function handleEditClick() {
    editable = !editable
  }

  // make the todo's name not editable
  function removeEdit() {
    editable = false
  }
</script>

<li>
  {#if !editable}
    <label class={done && "selected"}>
      <input type="checkbox" checked={done} on:change={handleChange} />
      {todoName}
    </label>
    <div>
      <button on:click={handleEditClick}>Edit</button>
      <button on:click={handleDelete} on:blur="{() => confirmed = false}" class="{!confirmed ? "danger" : "yellow"}">{!confirmed ? "Delete" : "Sure ??"}</button>
    </div>
  {:else}
    <form on:submit={handleSubmission}>
      <input
        type="text"
        checked={done}
        bind:value={todoName}
        on:blur={removeEdit}
      />
    </form>
  {/if}
</li>

<style>
  li {
    padding: 1em;
    background-color: #eee;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .selected {
    text-decoration: line-through;
  }

  button {
    cursor: pointer;
    background-color: white;
    padding: 10px 20px;
    border: none;
  }

  .danger {
    color: white;
    background-color: #fc5f5f;
  }

  .yellow {
    color: black;
    background-color: #fcff57;
  }
</style>
