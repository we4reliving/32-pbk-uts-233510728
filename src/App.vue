<template>
  <div class="app">
    <h1>📝 To-Do List</h1>

    <!-- Form Tambah Kegiatan -->
    <form @submit.prevent="addTodo" class="todo-form">
      <input
        v-model="newTodo"
        placeholder="Tambahkan kegiatan baru..."
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
    <ul v-if="filteredTodos.length" class="todo-list">
      <li v-for="(todo, index) in filteredTodos" :key="index" class="todo-item">
        <label>
          <input type="checkbox" v-model="todo.completed" />
          <span>{{ todo.text }}</span>
        </label>
        <button class="delete-btn" @click="removeTodo(index)">🗑</button>
      </li>
    </ul>
    <p v-else class="empty">Tidak ada kegiatan yang ditampilkan.</p>
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
/* Global */
body {
  background-color: #f0f4f8;
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

/* App Container */
.app {
  max-width: 600px;
  margin: 50px auto;
  padding: 30px;
  background-color: #ffffff;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
  text-align: center;
}

/* Judul */
h1 {
  margin-bottom: 24px;
  color: #2c3e50;
}

/* Form */
.todo-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.todo-form input {
  flex: 1;
  padding: 12px;
  border: 1px solid #dcdfe3;
  border-radius: 8px;
  font-size: 16px;
}
.todo-form button {
  padding: 12px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}
.todo-form button:hover {
  background-color: #369f75;
}

/* Filter */
.filter {
  text-align: left;
  margin-bottom: 15px;
  color: #34495e;
  font-size: 14px;
}
.filter input {
  margin-right: 8px;
}

/* Todo List */
.todo-list {
  list-style: none;
  padding: 0;
}
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #f8f9fa;
  padding: 12px 16px;
  margin-bottom: 10px;
  border-radius: 10px;
  transition: background 0.2s ease;
}
.todo-item:hover {
  background: #eef1f4;
}
.todo-item label {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
}
.todo-item input[type="checkbox"] {
  transform: scale(1.2);
}
.todo-item span {
  font-size: 16px;
  color: #2c3e50;
}

/* Delete Button */
.delete-btn {
  background: none;
  border: none;
  font-size: 18px;
  color: #e74c3c;
  cursor: pointer;
  transition: transform 0.2s ease;
}
.delete-btn:hover {
  transform: scale(1.2);
}

/* Empty Text */
.empty {
  font-style: italic;
  color: #888;
  margin-top: 20px;
}
</style>
