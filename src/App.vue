<template>
  <h1 @click="test">Hello !</h1>
  <form @submit.prevent="addNewTodo">
    <label>Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add new todo !</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <h3 :class="{ done: todo.done }" @click="test()"> {{todo.content}} </h3>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';
require('dotenv').config();

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function test() {
      console.log(process.env.apiKEY);
    }

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = ''
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    return {
      test,
      addNewTodo,
      newTodo,
      todos,
      toggleDone
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}
</style>
