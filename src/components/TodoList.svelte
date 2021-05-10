<script>
  import Todo from './Todo.svelte'
  import { todos } from '../store'
</script>

<ul>
  {#if $todos.length}
    {#each $todos as t,index }
      <Todo todoName={t.name} done={t.done} index={index} />
    {/each}
  {:else}
    <p>No todos today...</p>
  {/if}
</ul>

<style>
  ul {
    padding: 0;
    list-style: none;
    margin: 0;
  } 

  p {
    color: #9c9c9c;
  }
</style>