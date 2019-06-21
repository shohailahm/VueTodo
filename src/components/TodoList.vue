<template>
  <div class="hello">
    <h1>{{ msg }}</h1>"
    <input type="text" placeholder="whats need to be done?" class="input" v-model="newTodo" @keyup.enter="addTodo"/>
    <div class="row">
        <div class="inRow">
          <h4>Completed</h4>
          <ul v-cloak v-for="(todo,index) in todos" :key="todo" class="todoItem">
            <li v-if="todo.completed" @click="CompleteChange(index)">{{todo.item}}</li>
            <a v-if="todo.completed" @click="removeTodo(index)">Delete</a>
          </ul>
        </div>
        <div class="inRow">
          <h4>Pending</h4>
          <ul v-cloak v-for="(todo,index) in todos" :key="todo" class="todoItem">
            <li v-if="!todo.completed" @click="CompleteChange(index)">{{todo.item}}</li>
            <a v-if="!todo.completed" @click="removeTodo(index)">Delete</a>
          </ul>
        </div>
  
          <!-- {{todo}} -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  props: {
    msg: String
  },
  data(){
      return{
       newTodo:'',
       todos:[],
      }
  },
  methods:{
      addTodo(){
          this.todos.push({item:this.newTodo,completed:false,id:this.todos.length+1});
          this.newTodo="";
      },
      removeTodo(ind){
          this.todos.splice(ind,1);
      },
      CompleteChange(ind){
          this.todos[ind].completed=!this.todos[ind].completed
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.row{
    display: flex;
    flex-direction: row;
    width:100%;
    justify-content: space-around;

}
input{
    padding: 10px 18px;
    width:100%;
    font-size: 24px;
    border-radius: 5px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 10px;
  margin:10px;
}
.inRow{
    display: flex;
    justify-content: space-around;
    flex-direction: column;
}
li {
  display: inline-block;
  margin: 0 10px;
  cursor: pointer;
}
li:hover{
    color: red;
}
a {
  color: #42b983;
}
.todoItem{

}
</style>
