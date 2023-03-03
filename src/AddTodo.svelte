<script>
    export let onAddTodoHandler

    let newTodo = {
        todoTitle: '',
        todoDescription: "",
        isResolved: false
    }


    const onChangeTodoHandler = (field, value) => {
        newTodo = {...newTodo, [field]: value}
    }

</script>

<main>
    <form>
        <fieldset>
            <label for="todo-title">Todo Title</label>
            <input on:change={e => onChangeTodoHandler('todoTitle', e.currentTarget.value)} id="todo-title" name="todo-title" type="text">
        </fieldset>
        <fieldset>
            <label for="todo-description">Todo Description</label>
            <input on:change={e => onChangeTodoHandler('todoDescription', e.currentTarget.value)} id="todo-description" name="todo-description" type="text">
        </fieldset>
        <fieldset>
            <label for="todo-is-resolved">Is task resolved?</label>
            <input on:change={e => onChangeTodoHandler('isResolved', e.currentTarget.checked)} id="todo-is-resolved" name="todo-is-resolved" type="checkbox">
        </fieldset>
        <fieldset>
            <button on:click={e => onAddTodoHandler(newTodo, e)}>Add</button>
        </fieldset>
    </form>
</main>

<style>

    fieldset{
        border: none;
    }

    form{
        display: grid;
        place-items: center;
        background-color: white;
        box-shadow: 2px 2px 15px #ccc;
        width: 400px;
        height: fit-content;
        padding: 25px 15px;
        border-radius: 10px;
        
    }
</style>