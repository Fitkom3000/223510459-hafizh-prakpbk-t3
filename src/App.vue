<template>
  <div>
    <h1>To Do List</h1>
    <!-- Form untuk menambah kegiatan baru -->
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Tambah kegiatan baru" required>
      <button type="submit">Tambah</button>
    </form>

    <!-- Daftar kegiatan -->
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span>{{ todo.task }}</span>
        <button @click="editTodo(todo)">Edit</button>
        <button @click="deleteTodo(index)">Hapus</button>
      </li>
    </ul>

    <!-- Form untuk mengedit kegiatan -->
    <div v-if="editingTodo">
      <input type="text" v-model="editedTodo" required>
      <button @click="saveEdit">Simpan</button>
      <button @click="cancelEdit">Batal</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { task: 'Belajar Vue.js', completed: false },
        { task: 'Mengerjakan proyek', completed: true }
      ],
      newTodo: '',
      editingTodo: null,
      editedTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({ task: this.newTodo, completed: false });
      this.newTodo = '';
    },
    editTodo(todo) {
      this.editingTodo = todo;
      this.editedTodo = todo.task;
    },
    saveEdit() {
      this.editingTodo.task = this.editedTodo;
      this.cancelEdit();
    },
    cancelEdit() {
      this.editingTodo = null;
      this.editedTodo = '';
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style>
  /* Gaya umum */
  body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    padding: 20px;
  }
  h1 {
    color: #333;
    text-align: center;
  }

  /* Gaya untuk form dan daftar kegiatan */
  form {
    margin-bottom: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  input[type="text"] {
    padding: 8px;
    margin-right: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  button {
    padding: 8px 12px;
    border-radius: 5px;
    border: none;
    cursor: pointer;
    color: #fff;
    background-color: #f39c12; /* Warna emas */
  }
  button:hover {
    background-color: #e67e22; /* Warna emas tua */
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin-bottom: 10px;
    padding: 8px;
    border-radius: 5px;
    background-color: #fff; /* Warna putih */
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  li span {
    flex-grow: 1;
    color: #e67e22;
  }
</style>
