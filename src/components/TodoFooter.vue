<template>
  <footer>
    <button type="button" @click="finishRemove">완료일정 삭제</button>
    <button type="button" @click="allRemove">전체 삭제</button>
  </footer>
</template>

<script>
export default {
  name: "TodoFooter",
  methods : {
    finishRemove(){
      this.$emit("finishRemove")
    },
    allRemove(){
      this.$emit("allRemove")
    }
  }
};
</script>

<style lang="scss" scoped>
  footer {
    padding:30px; text-align:center; 
    button { background:#000; color:#fff; padding:10px;
      border-radius:5px; margin:0 10px; 
    }
  }
</style>
