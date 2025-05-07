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

    <!-- Tombol Filter -->
    <div class="filter">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <!-- Daftar Kegiatan -->
    <ul v-if="filteredTodos.length">
      <li v-for="(todo, index) in filteredTodos" :key="index">
        <label>
          <input type="checkbox" v-model="todo.completed" />
          {{ todo.text }}
        </label>
        <button class="delete-btn" @click="removeTodo(index)">Batal</button>
      </li>
    </ul>
    <p v-else>Tidak ada kegiatan yang ditampilkan.</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Data kegiatan awal
const todos = ref([
  { text: 'Belajar VueJS', completed: false },
  { text: 'Mengerjakan tugas UTS', completed: true },
  { text: 'Makan siang', completed: false }
])

const newTodo = ref('')
const showOnlyIncomplete = ref(false)

// Tambah kegiatan
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

// Filter kegiatan berdasarkan checkbox
const filteredTodos = computed(() => {
  return showOnlyIncomplete.value
    ? todos.value.filter(todo => !todo.completed)
    : todos.value
})
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
.filter {
  margin-top: 15px;
  text-align: left;
}
</style>
