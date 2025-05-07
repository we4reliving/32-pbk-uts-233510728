<template>
  <div class="app">
    <h1>To-Do List</h1>

    <!-- Form Tambah Kegiatan -->
    <form @submit.prevent="addTodo">
      <input
        v-model="newTodo"
        placeholder="Tambahkan kegiatan baru"
        required
      />
      <button type="submit">Tambah</button>
    </form>

    <!-- Daftar Kegiatan -->
    <ul v-if="todos.length">
      <li
        v-for="(todo, index) in todos"
        :key="index"
        :class="{ done: todo.completed }"
      >
        <label>
          <input
            type="checkbox"
            v-model="todo.completed"
          />
          {{ todo.text }}
        </label>
        <button class="delete-btn" @click="removeTodo(index)">Batal</button>
      </li>
    </ul>
    <p v-else>Belum ada kegiatan.</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Data kegiatan awal
const todos = ref([
  { text: 'Belajar VueJS', completed: false },
  { text: 'Mengerjakan tugas UTS', completed: true },
  { text: 'Makan siang', completed: false }
])

const newTodo = ref('')

// Tambahkan kegiatan baru
function addTodo() {
  const trimmed = newTodo.value.trim()
  if (trimmed !== '') {
    todos.value.push({ text: trimmed, completed: false })
    newTodo.value = ''
  }
}

// Hapus kegiatan
function removeTodo(index) {
  todos.value.splice(index, 1)
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

input[type="text"] {
  padding: 8px;
  width: 65%;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 8px 14px;
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
  background: #f9f9f9;
  padding: 10px;
  margin-bottom: 8px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
li.done label {
  text-decoration: line-through;
  color: #888;
}
label {
  flex: 1;
  cursor: pointer;
}
.delete-btn {
  background-color: #e74c3c;
}
.delete-btn:hover {
  background-color: #c0392b;
}
</style>
