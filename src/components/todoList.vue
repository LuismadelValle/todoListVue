<template>
    <div>
        <input type="text" class="todo-input" placeholder="Whats need to be done" v-model="newTodo" @keyup.enter="addTodo">
        <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
            <div class="todo-item-left">
                <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label">{{ todo.title }}</div>
                <input v-else class="todo-item-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)"
                @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>             
            </div>
            <div class="remove-item" @click="removeTodo(index)">
                &times;
            </div>            
        </div>
    </div>
</template>

<script>

const focus = {
  mounted: (el) => el.focus()
}

export default {
    name: 'todo-List',
    data() {
        return {
            newTodo: '',
            idForTodo: 4,
            beforeEditCache: '',
            todos: [
                {
                    'id': 1,
                    'title': 'Buy eggs',
                    'completed': false,
                    'editing': false,
                    
                }, {
                    'id': 2,
                    'title': 'Buy milk',
                    'completed': false,
                    'editing': false, 
                }, {
                    'id': 3,
                    'title': 'Buy Chocolate',
                    'completed': false,
                    'editing': false,
                }
            ]
        }
    }, 
   directives: {
    // enables v-focus in template
    focus
  },
    methods:  {
        addTodo() {
            // if(this.newTodo.trim().length = 0) {
            //     return
            // }

            this.todos.push({
                id: this.idForTodo,
                title: this.newTodo,
                completed: false
            })

            this.newTodo = ''
            this.idForTodo++
        },

        editTodo(todo) {
            this.beforeEditCache = todo.title
            todo.editing = true
        },

        doneEdit(todo) {
            if (todo.title.trim().length = 0) {
                todo.title = this.beforeEditCache
            }
            todo.editing = false
        },

        cancelEdit(todo) {
            todo.title = this.beforeEditCache
            todo.editing = false
        },

        removeTodo(index) {
            this.todos.splice(index, 1)
        }
    }
}

</script>

<style lang="scss">

.todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
 
    &:focus{
        outline: 0;
    }
}

.todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.remove--item {
    cursor: pointer;
    margin-left: 14px;
    &:hover {
        color: black; 
    }
}

.todo-item-edit {
    font-size: 18px;
    color: #2c3e50;
    // margin-left: 12px;
    width: 100%;
    padding: 10px 18px;
    border: 1px solid #ccc;
    // font-family: 'Avenir', Helvetica, Arial, sans-serif;

    &:focus {
        outline: none;
    }
}

</style>