<script>
    export let todoTitle = ''
    export let todoDescription = ''
    export let isResolved = false;
    export let todo_id;
    export let onDeleteTodoHandler
    $: taskStatus = isResolved ? "Resolved" : "Unresolved";
</script>


<main class="todo-wrapper">
    <article id={todo_id}> 
        <header>
            <h1 class="todo-header">{todoTitle}</h1>
        </header>
        <main>
            <p class='todo-info'>{todoDescription}</p>
            <span class={!isResolved ? 'unresolved' : "resolved"}>{taskStatus}</span>
            <button on:click={e => onDeleteTodoHandler(todo_id, e)} class="todo-delete-button">Delete</button>
        </main>

    </article>
</main>

<style>
    .todo-wrapper{
        display: grid;
        place-items: center;
        background-color: white;
        box-shadow: 2px 2px 15px #ccc;
        width: 700px;
        height: fit-content;
        padding: 25px 15px;
        border-radius: 10px;
    }
    .todo-header{
        font-size: 24px;
        color: black;
    }

    .todo-info{
        max-width: 500px;
        text-align: center;
        text-align-last: center;
        font-weight: 100;
        padding: 10px 0;
    }

    .resolved, .unresolved, .todo-delete-button{
        font-weight: 100;
        padding: 10px;
        border-radius: 10px;
        color: white;
        margin-bottom: 50px;
    }
    .resolved{
        background-color: lightseagreen;
       
    }

    .unresolved{
        background-color: lightcoral;
    }

    .todo-delete-button{
        cursor: pointer;
        background-color: rgb(242, 184, 11);
        border: none;
    }
</style>