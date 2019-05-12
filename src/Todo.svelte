<script>
    import { createEventDispatcher } from 'svelte';
    import { slide } from 'svelte/transition';

    export let id;
    export let text;
    export let done = false;

    const dispatch = createEventDispatcher();

    function dispatchDelete() {
        // use custom dispatch event for deleting entry in list
        dispatch('todo.delete', id);
    }

    function setDone() {
        done = !done;
    }
</script>

<style>
    .todo {
        display: grid;
        grid-template-areas: "a b";
        grid-template-columns: 80% 20%;
        transition: 170ms ease-in-out;
    }

    @media screen and (max-width: 768px) {
        .todo {
            grid-template-columns: 55% 45%;
        }
    }

    .text {
        width: calc(100% - 50px);
    }

    .data {
        grid-area: a;
        padding: 10px;
        background-color: purple;
        color: #fff;
    }
    .buttons {
        grid-area: b;
        display: grid;
        grid-template-areas: "done del";
        grid-template-columns: 50% 50%;
    }

    .btn {
        text-align: center;
        cursor: pointer;
        color: #fff;
        padding: 10px;
        transition: 120ms ease-in;
    }

    .done-btn {
        grid-area: done;
        background-color: #23c3ff;
    }
    .done-btn:hover {
        background-color: #1e90ff;
    }

    .done.done-btn {
        background-color: #3bc371;
    }
    .done.done-btn:hover {
        background-color: #389153;
    }

    .del-btn {
        grid-area: del;
        background-color: #ff4500;
    }
    .del-btn:hover {
        background-color: #de3e00;
    }
</style>

<div class="todo" in:slide out:slide>
    <div class="data">
        <span class="id">{id}</span>
        <span class="text">{text}</span>
    </div>
    <div class="buttons">
        <span class="btn done-btn" class:done={done} on:click={setDone}>{done ? 'finished' : 'not done'}</span>
        <span class="btn del-btn" on:click={dispatchDelete}>Delete</span>
    </div>
</div>

