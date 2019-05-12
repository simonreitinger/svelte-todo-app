<script>
    import Todo from './Todo.svelte';
    import { slide } from 'svelte/transition';

    let todos = [];
    let newText = '';
    let currentId = 0;

    function handleKeydown(e) {
        // key is not enter or text is empty
        if (e.which !== 13 || !newText) {
            return;
        }

        // use spread so svelte can render the list
        todos = [...todos, {id: ++currentId, text: newText}];
        newText = '';
    }

    function remove(e) {
        const removeId = e.detail;
        todos = todos.filter(((t) => t.id !== removeId));
    }
</script>

<style>
    #new input {
        outline: none;
        width: 100%;
        border: 1px solid purple;
    }
</style>

<div id="new">
    <input type="text" placeholder="Enter a Todo..." bind:value={newText} on:keydown={handleKeydown}>
</div>

<div id="list">
    {#each todos as todo}
        <Todo {...todo} on:todo.delete={remove}></Todo>
    {:else}
        <div in:slide out:slide>Nothing to do for now!</div>
    {/each}
</div>

