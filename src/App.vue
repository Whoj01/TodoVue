<template>
  <div id="app">
   <containerTodo/>
  </div>
</template>

<script>
import containerTodo from './components/containerTodo.vue'

export default {
  name: 'App',
  components: {
    containerTodo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
