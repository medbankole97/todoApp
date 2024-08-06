<template>
  <div class="todo-app">
    <h1>Vue 3 Todo App</h1>
    <form @submit.prevent="addNewTodo" class="todo-form">
      <label for="newTodo">New Todo</label>
      <input v-model="newTodo" name="newTodo" placeholder="Enter a new task" />
      <button>Add New Todo</button>
    </form>
    <div class="actions">
      <button @click="removeAllTodos">Remove All</button>
      <button @click="markAllDone">Mark All Done</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <h3 :class="{done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
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
        done: false,
        content: newTodo.value,
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
      todos.value.forEach(todo => todo.done = true);
    }

    function removeAllTodos() {
      todos.value = [];
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  }
};
</script>
<style scoped>
body {
  font-family: 'Arial', sans-serif;
  background-color: #f4f4f9;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
 
}

.todo-app {
  background: white;
  padding: 2em;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  width: 100%;
  margin: auto;
 
}

h1 {
  text-align: center;
  color: #333;
}

.todo-form {
  display: flex;
  flex-direction: column;
  margin-bottom: 1em;
}

.todo-form input {
  padding: 0.5em;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-bottom: 1em;
  font-size: 1em;
}

.todo-form button {
  padding: 0.5em;
  background-color: #2253be;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1em;
}

.todo-form button:hover {
  background-color: #4cae4c;
}

.actions {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1em;
}

.actions button {
  padding: 0.5em;
  background-color: #d9534f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1em;
  width: 48%;
}

.actions button:hover {
  background-color: #c9302c;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5em 0;
  border-bottom: 1px solid #ddd;
}

.todo-item h3 {
  margin: 0;
  cursor: pointer;
  flex-grow: 1;
  padding-right: 1em;
}

.todo-item h3.done {
  text-decoration: line-through;
  color: #aaa;
}

.todo-item button {
  background-color: #d9534f;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
  padding: 0.3em 0.5em;
}

.todo-item button:hover {
  background-color: #c9302c;
}
</style>
