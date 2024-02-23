<template>
  <footer>
    <button type="button" @click="allRemove">완료일정 삭제</button>
  </footer>
</template>

<script>
export default {
  name: "TodoFooter",
};
</script>

<style lang="scss" scoped>
  footer {
    padding:30px; text-align:center; 
    button { background:#000; color:#fff; padding:10px;
      border-radius:5px
    }
  }
</style>
