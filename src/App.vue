<template>
  <div id="app">
    <TodoInput @add="addTodo" />
    <TodoList :todos="todos" @delete="deleteTodo" />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

import TodoInput from '@/components/TodoInput.vue';
import TodoList from '@/components/TodoList.vue';

export default {
  components: {
    TodoInput,
    TodoList,
  },
  setup() {
    const todos = ref([]);

    const fetchTodos = () => {
      axios
        .get('http://localhost:8080/api/todos')
        .then((response) => {
          todos.value = response.data;
        })
        .catch((error) => {
          console.error('Error fetching todos:', error);
        });
    };

    const addTodo = (task) => {
      axios
        .post('http://localhost:8080/api/todos', { task })
        .then((response) => {
          todos.value.push(response.data);
        })
        .catch((error) => {
          console.error('Error adding todo:', error);
        });
    };

    const deleteTodo = (id) => {
      axios
        .delete(`http://localhost:8080/api/todos/${id}`)
        .then(() => {
          todos.value = todos.value.filter((todo) => todo.id !== id);
        })
        .catch((error) => {
          console.error('Error deleting todo:', error);
        });
    };

    onMounted(() => {
      fetchTodos();
    });

    return {
      todos,
      addTodo,
      deleteTodo,
    };
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 2em;
}
</style>
