<template>
        <!-- <p v-if="loadingData">Loading Data.......</p>
        <p v-else-if="todosExist">No data found</p> -->
        <p v-if="deletedSuccessfully" :class="{'delete-success': deletedSuccessfully}">{{ deleteMessage }}</p>
        <todo-item v-for="todo in todos" :key="todo.id"
                :id="todo.id"
                :title="todo.title"
                :description="todo.description"
                :status="todo.status"
                :priority="todo.priority"
                @delete-todo="deleteTodoItem">
        </todo-item>
        
        
</template>

<script>
import TodoItem from './TodoItem.vue'
import axios from 'axios'

export default {
    data(){
        return {
            todos: [],
            loadingData: false,
            deleteMessage: null
        }
    },
    computed: {
        deletedSuccessfully(){
            return this.deleteMessage !== null
        },
        todosExist(){
            return this.loadingData === false && this.todos && this.todos.length > 0
        }
    },
    components: {
        TodoItem
    },
    methods: {
        fetchTodos(){
        this.loadingData = true
        axios.get("https://todo-app-7a0f5-default-rtdb.firebaseio.com/todos.json")
        .then((response) => {
            if (response.status === 200 && response.data !== null){
                return response.data
            }
        }).then((data) => {
            this.loadingData = false
            const results = []
            for (const id in data){
                results.push({
                    id: id,
                    title: data[id].title,
                    description: data[id].description,
                    status: data[id].status,
                    priority: data[id].priority,
                })
            }
            this.todos = results
        }).catch(error => {
            this.loadingData = false
            console.log(error)
            this.fetchError = true
        })
    },
    deleteTodoItem(id){
        axios.delete('https://todo-app-7a0f5-default-rtdb.firebaseio.com/todos/' + id.toString() + '.json')
        .then(response => {
            if (response.status === 200){
                this.deleteMessage = "Task deleted successfully"
            }
            
      });
    }
    },
    mounted(){
        this.fetchTodos()
    }
}
</script>

<style scoped>
.delete-success {
    color: green;
}
</style>