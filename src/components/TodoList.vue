<template>
  <section>
    <transition-group name="list" tag="ul">
        <li v-for="item in todos" :key="item.id">
          <input type="checkbox" v-model="item.modify" @click="onToggle(item.id)">
          <label :for="item.id"><i :class="{'fa-solid':true, 'fa-pen-to-square':item.update, 'fa-floppy-disk':!item.update}" @click="onUpdate(item.id)"></i></label>
          {{ item.id }}번 <input :id="item.id" type="text" :class="{on:item.modify}" :value="item.text" :disabled="item.update" @input="onInput(item.id, $event)" />
          <button type="button" @click="onRemove(item.id)">
            <i class="fa-solid fa-trash-can"></i>
          </button>
        </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  name: "TodoList",
  props:['todos'],
  methods:{
    onRemove(id) {
      let answer = confirm("정말로 삭제하시겠습니까?")
      if (answer) {
        this.$emit("onRemove", id)
      }
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
        input[type=text] { flex:1; padding:5px; margin:0 10px; 
          font-size:20px; background:none; 
          &.on { text-decoration:line-through; color:#999 }
        }
        button { color:red; font-size:20px;  }
      }
    }
  }

.list-enter-active, .list-leave-active {
    transition:all 0.5s;
}
.list-enter, .list-leave-to {
    opacity:0;
    // transform:translateX(50px)
    transform:scale(0.5)
}

</style>
