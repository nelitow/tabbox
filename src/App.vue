<template>
  <form @submit.prevent="addNewTodo">
    <label for=""> New todo</label>
    <input v-model="newTodo" type="text" name="newTodo">
    <button>Add new todo</button>
  </form>
  <button @click="markAllDone">Mark all done</button>
  <button @click="removeAll">Remove all</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id">
      <h3 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button @click="removeTodo(index)">Remove todo</button>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  setup(){
    const newTodo = ref('');
    const todos = ref([]); 
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value
      });
      newTodo.value = null;
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

    function removeAll() {
      todos.value = [];
    }

    return {
      toggleDone,
      newTodo,
      todos,
      addNewTodo,
      removeTodo,
      markAllDone,
      removeAll,
    };
  }
}
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
