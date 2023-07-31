<script>
  import TodoForm from "./lib/TodoForm.svelte";

  let todoList = localStorage.getItem('todoList') ? JSON.parse(localStorage.getItem('todoList')) : [];

  function addTodo (todo) {
    todoList.push({
      'title': todo,
      'done': false,
    })
    todoList = todoList
  }

  function deleteTodo(i){
    todoList.splice(i, 1)
    todoList = todoList;
  }

  $: localStorage.setItem('todoList', JSON.stringify(todoList));
</script>

<main>
  <TodoForm {addTodo}/>
  <ul>
    {#each todoList as {title, done}, index}
    <li class="todo">
      {#if done}
        <span>✅</span>
      {/if}
      <span class:done={done} on:click={() => done = !done}>{title}</span>
      <span class="delete" on:click={() => deleteTodo(index)}>🗑️</span>
    </li>
    {/each}
    
  </ul>
</main>

<style>
  .todo {
    cursor: pointer;
  }
  .done{
    text-decoration: line-through;
  }
  .delete {
    display: inline-block;
  }
  .delete:hover{
    transform: scale(2);
  }
</style>
