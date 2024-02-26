<template>
  <section>
    <ul>
      <li v-for="item in todos" :key="item.id">
        <input type="checkbox" v-model="item.modify" @click="onToggle(item.id)">
        <label :for="item.id"><i :class="{'fa-solid':true, 'fa-pen-to-square':item.update, 'fa-floppy-disk':!item.update}" @click="onUpdate(item.id)"></i></label>
        {{ item.id }}번 <input :id="item.id" type="text" :class="{on:item.modify}" :value="item.text" :disabled="item.update" @input="onInput(item.id, $event)" />
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
    },
    onUpdate(id){
      this.$emit("onUpdate", id)
    },
    onInput(id, e){
      this.$emit("onInput", id, e.target.value)
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
        align-items:center; 
        label { margin:0 10px }
        input[type=text] { flex:1; line-height:50px; margin:0 10px; font-size:20px;
          &.on { text-decoration:line-through; color:#999 }
        }
        button { color:red; font-size:20px;  }
      }
    }
  }
</style>
