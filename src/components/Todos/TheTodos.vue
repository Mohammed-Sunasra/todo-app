<template>
  <base-card>
    <base-button @click="setActiveTab('todo-list')" :mode="todoListMode">TodoList</base-button>
    <base-button @click="setActiveTab('add-todo')" :mode="addTodoMode">AddTodo</base-button>
    <keep-alive>
    <component :is="selectedTab"></component>
    </keep-alive>
    <p v-if="fetchError">Error while fetching data</p>
  </base-card>
</template>

<script>

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
    }
  }
};
</script>
