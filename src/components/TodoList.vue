<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
        <div  @dragover.prevent @drop.prevent @drop="dragFinish(-1, $event)" v-if="dragging > -1" class="trash-drop todo-item" >
          Delete
          </div>
    
    <div v-else>
       <input type="text" placeholder="whats need to be done?" class="input" v-model="newTodo" @keyup.enter="addTodo"/>
    </div>
  
    <div class="row">
        <div class="inRow">
          <h4>Completed</h4>
          <ul v-cloak v-for="(todo,index) in todos" :key="index" class="todoItem">
            <li v-if="todo.completed" @click="CompleteChange(index)">{{todo.item}}</li>
            <a v-if="todo.completed" @click="removeTodo(index)">Delete</a>
          </ul>
        </div>
        <div class="inRow">
          <h4>Pending</h4>
          <ul v-cloak v-for="(todo,index) in todos" :key="index" class="todoItem">
            <div draggable="true" @dragstart="dragStart(index, $event)" @dragover.prevent @dragenter="dragEnter" @dragleave="dragLeave" @dragend="dragEnd" @drop="dragFinish(index, $event)">
              <li v-if="!todo.completed" @click="CompleteChange(index)">{{todo.item}}</li>
              <a v-if="!todo.completed" @click="removeTodo(index)">Delete</a>
            </div>

          </ul>
        </div>
  
          <!-- {{todo}} -->
    </div>
  </div>
</template>

<script>
import { defaultCoreCipherList } from 'constants';
export default {
  name: 'todo-list',
  props: {
    msg: String
  },
  data(){
      return{
       newTodo:'',
       todos:[],
       dragging: -1
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
      },
      dragStart(i,ev){
        this.dragging = 1;
        //  ev.dataTransfer.setData('Text', this.id);
         ev.dataTransfer.dropEffect = 'move'
         
      },dragEnter(ev) {
      /* 
      if (ev.clientY > ev.target.height / 2) {
        ev.target.style.marginBottom = '10px'
      } else {
        ev.target.style.marginTop = '10px'
      }
      */
    },removeItemAt(index) {
      this.todos.splice(index, 1);
    },
    dragLeave(ev) {
      
      /* 
      ev.target.style.marginTop = '2px'
      ev.target.style.marginBottom = '2px'
      */
    },
    dragEnd(ev) {
      ev.preventDefault()
      
      this.dragging = -1;
    },
    dragFinish(to, ev) {
      
      this.moveItem(this.dragging, to);
      ev.target.style.marginTop = '2px'
      ev.target.style.marginBottom = '2px'
    },
    moveItem(from, to) {
      
      if (to === -1) {
        this.removeTodo(from);
        return this.dragging=1;
      } else {
        this.todos.splice(to, 0, this.todos.splice(from, 1)[0]);
      }
    }
  },

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
.trash-drop {
  border: 2px dashed #ccc !important;
  text-align: center;
  color: #e33;
}
</style>
