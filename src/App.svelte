<script>
    import AddTodo from './AddTodo.svelte';
    import Todo from './Todo.svelte';
    import { v4 as uuidv4 } from 'uuid';

    let todoList = [];

    try {
        const savedTodos = localStorage.getItem('todos');
		const parsedTodos = JSON.parse(savedTodos);

		if(parsedTodos.length){
			todoList =  parsedTodos;
		}else{
			todoList = []
		}
        
    } catch (e) {
        todoList = [];
    }

    let isFormShown = false;
    let uuid = '';

    $: formBttonText = isFormShown ? 'Show my todos' : 'Add todo';

    const onFormOpenAction = () => (isFormShown = !isFormShown);

    const onAddTodoHandler = (todo, event) => {
        event.preventDefault();
        uuid = uuidv4();

		
        todoList = [...todoList, { ...todo, id: uuid }];

        localStorage.setItem('todos', JSON.stringify(todoList));
    };

    const onDeleteTodoHandler = (todo_id, event) => {
        event.preventDefault();
        todoList = todoList.filter((todo) => todo.id !== todo_id);

        localStorage.setItem('todos', JSON.stringify(todoList));
    };
</script>

<main>
    <h1>My todo list</h1>
    <button on:click={onFormOpenAction}>{formBttonText}</button>
    <section class="todo-list">
        {#if isFormShown}
            <AddTodo {onAddTodoHandler} />
        {:else if todoList?.length}
            {#each todoList as todo}
                <Todo
                    todo_id={todo.id}
                    {onDeleteTodoHandler}
                    todoDescription={todo.todoDescription}
                    todoTitle={todo.todoTitle}
                    isResolved={todo.isResolved}
                />
            {/each}
        {:else}
            <p>You didn't add any todo :(</p>
        {/if}
    </section>
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    .todo-list {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        justify-content: center;
    }
    button {
        border: none;
        padding: 10px 15px;
        margin-bottom: 25px;
        font-size: 18px;
        border-radius: 12px;
        cursor: pointer;
    }
    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
