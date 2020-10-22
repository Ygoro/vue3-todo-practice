<template>
  <div>
    <form @submit.prevent="addNewTodo">
      <label>Add New Todo:</label>
      <input v-model="newTodo" name="newTodo">
      <button>Add</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
        <button @click="removeTodo(index)">Remove Todo</button>
      </li>
    </ul>
    <button @click="removeAllTodos">Remove All Todos</button>
    <button @click="markAllDone">Mark All Done</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        content: newTodo.value,
        done: false,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = true);
    }

    function removeAllTodos() {
      todos.value = [];
    }

    return {
      newTodo,
      addNewTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    }
  }
}
</script>

<style>
body {
  font-family: sans-serif;
  font-size: 2em;
  width: 80%;
  padding-top: 1em;
  padding-bottom: 1em;
  margin: 0 auto;
}
input, div, button {
  font-family: sans-serif;
  font-size: 1em;
  display: block;
  width: 100%;
  margin: 0.5em;
}
.todo {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
