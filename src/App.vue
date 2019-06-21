<template>
  <div id="app" class="container">
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    
     <todo-list msg="Welcome to Your Vue.js ToDoList App"></todo-list>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TodoList from './components/TodoList.vue'
export default {
  name: 'app',
  components: {
    HelloWorld,
    TodoList
  }
}
</script>

<style>
*{
  box-sizing: border-box;
}
.container{
  max-width: 600px;
  margin:0 auto;
}
.logo{
  height:100px;
  width:100px;

}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
