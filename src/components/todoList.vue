<template>
    <div>
        Todo List of Luis Manuel
        <input type="text" class="todo-input" placeholder="Whats need to be done" v-model="newTodo">
    </div>
</template>

<script>

export default {
    name: 'todo-List',
    data() {
        return {
            newTodo: '',
            todos: [
                {
                    'id': 1,
                    'title': 'Buy eggs',
                    'completed': false
                    
                }, {
                    'id': 2,
                    'title': 'Buy milk',
                    'completed': false 
                }, {
                    'id': 3,
                    'title': 'Buy Chocolate',
                    'completed': false
                }
            ]
        }
    }
}

</script>

<style lang="scss">

.todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-button: 16px;

    &:focus{
        outline: 0;
    }
}

</style>