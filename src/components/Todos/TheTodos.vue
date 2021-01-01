<template>
  <base-card>
    <base-button @click="setActiveTab('todo-list')" :mode="todoListMode">TodoList</base-button>
    <base-button @click="setActiveTab('add-todo')" :mode="addTodoMode">AddTodo</base-button>
    <component :is="selectedTab"></component>
    <p v-if="fetchError">Error while fetching data</p>
  </base-card>
</template>

<script>
import axios from 'axios'
import AddTodo from './AddTodo.vue';
import TodoList from './TodoList.vue';

export default {
  components: {
    AddTodo,
    TodoList
  },
  computed: {
      todoListMode(){
          return this.selectedTab === 'todo-list' ? null : 'flat'
      },
      addTodoMode(){
          return this.selectedTab === 'add-todo' ? null : 'flat'
      },
  },
  data() {
    return {
        selectedTab: 'todo-list',
        todos: [],
        fetchError: false
    };
  },
  methods: {
    setActiveTab(tabName) {
      this.selectedTab = tabName;
    },
    
    fetchTodos(){
        axios.get("https://todo-app-7a0f5-default-rtdb.firebaseio.com/todos.json")
        .then((response) => {
            // console.log(response)
            if (response.status === 200 && response.data !== null){
                return response.data
            }
        }).then((data) => {
            // console.log(data)
            const results = []
            for (const id in data){
                results.push({
                    id: data[id],
                    title: data[id].title,
                    description: data[id].description,
                    status: data[id].status,
                    priority: data[id].priority,
                })
            }
            // console.log(results)
            this.todos = results
        }).catch(error => {
            console.log(error)
            this.fetchError = true
        })
    }
  }
};
</script>
