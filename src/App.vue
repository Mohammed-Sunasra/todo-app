
<template>
  <the-header title="Task Management App"></the-header>
  <the-todos></the-todos>
</template>

<script>
import TheTodos from './components/Todos/TheTodos.vue'
import TheHeader from './components/layout/TheHeader.vue'
export default {
  components: {
    TheTodos,
    TheHeader
  }
}
</script>


<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}
</style>