<template>
  <div id="app">
   <tab />
   <todos />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import tab from './components/tab.vue'
import todos from './components/todos.vue'

export default {
  name: 'App',
  components: {
    tab,
    todos
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
