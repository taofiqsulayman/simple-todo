<script>

import { fade, fly } from 'svelte/transition';
import { flip } from 'svelte/animate';

let todos = [];
let inputValue;

const addTodo = () => {
  if (inputValue) {
    let newTodo = {
      title: inputValue,
      id: todos.length + 1,
    };

    todos = [newTodo, ...todos];
    inputValue = "";
  }

}

const deleteTodo = (id) => {
  todos = todos.filter((todo) => todo.id !== id);
}

</script>

<div class="container">
  <form on:submit|preventDefault={addTodo}>
    <input type="text" bind:value={inputValue} />
    <button on:click={addTodo}>Add Task</button>
  </form>

  {#each todos as todo (todo.id) }
    <div class="todo" animate:flip={{duration:150}} in:fade out:fly={{duration:150}}>
      <h3>{todo.title}</h3>
      <button on:click={() => deleteTodo(todo.id)}>Remove</button>
    </div>
  {/each}
</div>




<style>

  .container {
    padding-left: 15%;
    padding-right: 15%;
  }

  form {
		display: flex;
    justify-content: space-between;
    margin: 10px;
	}
	
	form input {
		/* flex-grow: 1; */
    min-width: 85%;
		box-sizing: border-box;
		border-radius: 4px;
		padding: 1em;
		font-size: inherit;
	}
	
	form button {
		border-radius: 4px;
    color: whitesmoke;
    background-color: rgb(7, 156, 106);
		border: 1px solid rgba(0,0,0,0.1);
	}
	
	button {
		padding: 1em;
		border: none;
		box-sizing: border-box;
		font-family: inherit;
		font-size: inherit;
		line-height: 1;
		width: 6em;
	}

  .todo {
		position: relative;
		width: 100%;
		padding: 1em;
		line-height: 1;
		box-shadow: 2px 4px 8px rgba(0,0,0,0.1);
		border-radius: 4px;
		margin: 0 0 0.5em 0;
		border: 1px solid rgba(0,0,0,0.1);
		box-sizing: border-box;
		text-transform: uppercase;
	}
	
	.todo button {
		position: absolute;
		right: 0;
		top: 0;
		background: rgba(255,255,255,0.4);
    color: red;
	}
	
	.todo button:hover {
		background: rgba(241, 50, 50, 0.2);
	}
</style>