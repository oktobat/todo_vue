<template>
  <section>
    <ul>
      <li v-for="item in todos" :key="item.id">
        <input type="checkbox" v-model="item.modify" @click="onToggle(item.id)">
        <span :class="{on:item.modify}">{{ item.id }}번 {{ item.text }}</span>
        <button type="button" @click="onRemove(item.id)">
          <i class="fa-solid fa-trash-can"></i>
        </button>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "TodoList",
  props:['todos'],
  methods:{
    onRemove(id) {
      this.$emit("onRemove", id)
    },
    onToggle(id){
      this.$emit("onToggle", id)
    }
  }
};
</script>

<style lang="scss" scoped>
  section {
    ul {
      li {
        display:flex;
        height:50px; 
        margin:5px 0; 
        padding:0 16px; 
        border-bottom:1px solid #ddd; 
        span { flex:1; line-height:50px; margin:0 10px; font-size:20px;
          &.on { text-decoration:line-through; color:#999 }
        }
        button { color:red; font-size:20px;  }
      }
    }
  }
</style>
