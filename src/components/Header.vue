<template>
  <header class="header">
      <h1>Danh Sach User</h1>
      <!-- <AddTodo /> -->
  </header>
</template>

<script>
import AddTodo from './AddTodo.vue';
export default {
    name: "Header",
    setup() {
        return {
            AddTodo
        }
    }
}
</script>

<style scoped>
.header {
    background: #333;
    color: #fff;
    text-align: center;
    padding: 10px;
}
</style>