<template>
  <div id="container">
    <TodoHeader :todos="todos"></TodoHeader>
    <TodoInput @addTodo="addTodo"></TodoInput>
    <TodoList :todos="todos" @onRemove="onRemove" @onToggle="onToggle" @onUpdate="onUpdate" @onInput="onInput"></TodoList>
    <TodoFooter @finishRemove="finishRemove" @allRemove="allRemove"></TodoFooter>
  </div>
</template>

<script>
import "./assets/css/reset.css";
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "App",
  data(){
    return { 
      flag:true,
      id:0,
      todos : [ 
        // {id:0, text:'할일1', modify:false, update:true },
        // {id:1, text:'할일2', modify:true, update:true },
        // {id:2, text:'할일3', modify:false, update:true },
      ]
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  },
  created(){
    let id = localStorage.getItem("id")
    let todos = JSON.parse(localStorage.getItem("todos"))
    if (id){
      this.id = id
    }
    if (todos) {
      this.todos = todos
    } else {
      this.todos = []
    }
  },
  methods:{
    addTodo(text){
      // console.log(text)
      this.todos.push({ id:this.id, text:text, modify:false, update:true })
      this.id++
      localStorage.setItem("id", this.id)
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
    onRemove(id) {
      this.todos = this.todos.filter((value)=> value.id !== id )
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
    finishRemove(){
      this.todos = this.todos.filter((value)=>{
        return value.modify == false
      })
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
    allRemove(){
      // this.todos = []
      this.todos.splice(0, this.todos.length)

      // localStorage.setItem("todos", JSON.stringify(this.todos))
      localStorage.removeItem("todos")
    },
    onToggle(num){
      this.todos.map((item)=>{
        if (item.id == num) {
          item.modify = !item.modify
        }
      })
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
    onUpdate(num){
        this.todos.map((item)=>{
          if (item.id == num) {
            item.update = !item.update
          } else {
            item.update = true
          }
       })
       localStorage.setItem("todos", JSON.stringify(this.todos))      
    },
    onInput(num, text){
      this.todos.map((item)=>{
          if (item.id == num) {
            item.text = text
          }
       })
    }
  }
};
</script>

<!-- scoped 속성을 가지고 있으면, css는 현재 컴포넌트의 요소에만 적용 -->
<style scoped>
#container {
  max-width: 600px;
  margin: 50px auto;
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  background:#fff; 
}
</style>
