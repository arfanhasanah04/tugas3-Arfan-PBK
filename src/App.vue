<template>
  <div class="app">
    <header>
      <h1>My Daily Journal</h1>
      <input type="text" v-model="newTodo" @keyup.enter="addTodo" placeholder="Tambahkan kegiatan">
      <input type="date" v-model="newDate">
    </header>
    <main>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.completed">
          <span :class="{ 'completed': todo.completed }">{{ todo.text }}</span>
          <button @click="deleteTodo(index)">Hapus</button>
        </li>
      </ul>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const todos = ref([
  { text: '', completed: false, date: '2024-05-12' },
  { text: '', completed: true, date: '2024-05-12' },
  { text: '', completed: false, date: '2024-05-12' }
]);

const newTodo = ref('');
const newDate = ref('');

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({ text: newTodo.value, completed: false, date: newDate.value });
    newTodo.value = '';
    newDate.value = '';
  }
}

function deleteTodo(index) {
  todos.value.splice(index, 1);
}
</script>

<style scoped>
/* Gaya CSS Anda di sini */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');

body {
  font-family: 'Poppins', sans-serif;
  margin: 0;
  padding: 0;
}

.app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff8e1; /* Warna krim */
  border-radius: 10px;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

h1 {
  color: #85522e;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

input[type="text"],
input[type="date"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid #8b0d0d;
  border-radius: 5px;
}

input[type="checkbox"] {
  margin-right: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  padding: 10px;
  background-color: #fff;
  border-radius: 5px;
  display: flex;
  align-items: center;
}

.completed {
  text-decoration: line-through;
}

button {
  background-color: #db812ccf;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  margin-left: auto;
}

button:hover {
  background-color: #e2d9d9;
}

main {
  background-image: url('https://via.placeholder.com/600x400');
  background-size: cover;
  background-position: center;
  border-radius: 10px;
  padding: 20px;
}
</style>
