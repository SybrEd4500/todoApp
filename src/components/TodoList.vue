<template>
  <div class="todo-list">
    <div v-for="todo in todos" :key="todo.id" class="todo-item">
      {{ todo.task }}
      <button @click="deleteTodo(todo.id)">Delete</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  props: {
    todos: Array,
  },
  methods: {
    deleteTodo(id) {
      this.$emit('delete', id);
    },
  },
};
</script>

<style scoped>
.todo-list {
  display: flex;
  margin-top: 20px;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid#ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  max-width: 300px;
  width: 100%;
}

.todo-item button {
  padding: 8px;
  font-size: 14px;
  background-color: #d9534f;
  color: #fff;
  border: none;
  cursor: pointer;
}
</style>
