<template>
  <div class="app">
    <h1>To-Do List</h1>

    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="Tambahkan kegiatan baru" />
    </form>

    <ul v-if="todos.length">
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
      </li>
    </ul>
    <p v-else>Belum ada kegiatan.</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const todos = ref([
  'Belajar VueJS',
  'Mengerjakan tugas UTS',
  'Makan siang'
])

const newTodo = ref('')

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push(newTodo.value.trim())
    newTodo.value = ''
  }
}
</script>

<style scoped>
.app {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  font-family: sans-serif;
  text-align: center;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
input {
  padding: 8px;
  width: 70%;
  margin-right: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
button {
  padding: 8px 12px;
  border: none;
  background-color: #42b983;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #369f75;
}
ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;
  text-align: left;
}
li {
  background: #f5f5f5;
  padding: 10px;
  margin-bottom: 8px;
  border-radius: 5px;
}
</style>
