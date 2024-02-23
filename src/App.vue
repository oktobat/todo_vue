<template>
  <div id="container">
    <TodoHeader></TodoHeader>
    <TodoInput @addTodo="addTodo"></TodoInput>
    <TodoList :todos="todos" @onRemove="onRemove"></TodoList>
    <TodoFooter></TodoFooter>
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
      id:0,
      todos : [ 
        // {id:0, text:'할일1', modify:false },
        // {id:1, text:'할일2', modify:true },
        // {id:2, text:'할일3', modify:false },
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
      this.todos = todos
    }
  },
  methods:{
    addTodo(text){
      // console.log(text)
      this.todos.push({ id:this.id, text:text, modify:false })
      this.id++
      localStorage.setItem("id", this.id)
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
    onRemove(id) {
      this.todos = this.todos.filter((value)=> value.id !== id )
      localStorage.setItem("todos", JSON.stringify(this.todos))
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
