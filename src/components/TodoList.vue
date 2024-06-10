<template>
    <div class="todo-list">
      <h1>Todo List</h1>
      <input v-model="newTodo" placeholder="Add a new task" @keyup.enter="addTodo" />
      <button @click="addTodo">Add</button>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <span :class="{ completed: todo.completed }" @click="toggleTodoCompletion(index)">
            {{ todo.text }}
          </span>
          <button @click="deleteTodo(index)">Delete</button>
        </li>
      </ul>
      <p>{{ incompleteTodos }} tasks remaining</p>
    </div>
  </template>
  
  <script>
  import { useTodoStore } from '../stores/todoStore';
  import { computed, ref } from 'vue';
  
  export default {
    setup() {
      const store = useTodoStore();
      const newTodo = ref('');
  
      const addTodo = () => {
        if (newTodo.value.trim()) {
          store.addTask(newTodo.value);
          newTodo.value = '';
        }
      };
  
      const deleteTodo = (index) => {
        store.removeTask(index);
      };
  
      const toggleTodoCompletion = (index) => {
        store.toggleTaskStatus(index);
      };
  
      return {
        newTodo,
        todos: computed(() => store.tasks),
        addTodo,
        deleteTodo,
        toggleTodoCompletion,
        incompleteTodos: computed(() => store.incompleteTasksCount),
      };
    },
  };
  </script>
  <style scoped>
  .todo-list {
    max-width: 400px;
    margin: 50px auto;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15); /* Bayangan yang lebih besar */
    background-color: #e4bcf5; /* Warna latar belakang */
    font-family: 'Poppins', sans-serif; /* Menggunakan font Poppins */
    text-align: center; /* Mengatur tampilan ditengah */
    transform-style: preserve-3d; /* Menjaga 3D effect pada elemen child */
    perspective: 1000px; /* Menentukan perspektif */
  }
  
  h1 {
    color: #333; /* Warna teks judul */
  }
  
  input, button, ul {
    transform-style: preserve-3d; /* Menjaga 3D effect pada elemen child */
  }
  
  input {
    width: calc(100% - 70px);
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #be2222;
    border-radius: 5px;
    background-color: #ffffff; /* Warna latar belakang input */
    transition: transform 0.3s ease; /* Animasi saat hover */
  }
  
  button {
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    background-color: #05c9ff; /* Warna tombol */
    color: #fff;
    cursor: pointer;
    transition: transform 0.3s ease; /* Animasi saat hover */
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); /* Bayangan yang lebih kompleks */
  }
  
  button:hover {
    transform: translateY(-3px); /* Menggeser tombol ke atas */
    background-color: #e7e9e9;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 0;
    border-bottom: 1px solid #ccc;
    transition: transform 0.3s ease; /* Animasi saat hover */
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); /* Bayangan yang lebih kompleks */
  }
  
  li:hover {
    transform: translateY(-3px); /* Menggeser item daftar ke atas */
  }
  
  li .completed {
    text-decoration: line-through;
    color: #14da52; /* Warna teks tugas yang sudah selesai */
  }
  
  span {
    cursor: pointer;
  }
  </style>
  