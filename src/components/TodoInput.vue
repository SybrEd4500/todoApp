<template>
  <div class="todo-input">
    <input v-model="task" placeholder="Enter task" />
    <button @click="addTodo">Add</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup(_, context) {
    const task = ref('');

    const addTodo = () => {
      context.emit('add', task.value);
      task.value = '';
    };

    return {
      task,
      addTodo,
    };
  },
};
</script>

<style scoped>
.todo-input {
  display: flex;
  margin-bottom: 10px;
  max-width: 300px;
  align-items: center;
  margin: 0 auto; /* 中央に配置 */
}

.todo-input input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
}

.todo-input button {
  margin-left: 10px;
  padding: 8px 12px;
  font-size: 16px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  cursor: pointer;
}
</style>
