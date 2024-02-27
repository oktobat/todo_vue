<template>
  <header>
    <h1>일정관리앱 {{ complete }}/{{ total }}건 처리</h1>
  </header>
</template>

<script>
export default {
  name: "TodoHeader",
  props:["todos"],
  computed:{
    complete(){
        return this.todos.filter(item=>item.modify==true).length
    },
    total(){
        return this.todos.length
    }
  }
};
</script>

<style scoped>
h1 {
  background: #22b8cf;
  color: #fff;
  font-size: 24px;
  text-align: center;
  padding: 20px;
}
</style>
