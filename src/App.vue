<script setup>
import {ref} from 'vue'

let todos = ref([])
let NewTodos = ref('')

function AddTodo () { 
  todos.value.push({
    text: NewTodos.value,
    complete: false
  })
  NewTodos.value = ''
}

function DeleteTodos (index) {
    todos.value.splice(index, 1)

  }
</script>

<template>
  <body>
<h1>My Todo Application</h1>

<ul>
<li v-for="(todo, index) in todos">
  <input type="checkbox" v-model="todo.complete">
  <button @click="DeleteTodos">🚮</button>
  {{ todo.text }}
</li>
</ul>

<input v-model="NewTodos" @keydown.enter="AddTodo">
<button @click="AddTodo">Add Todo</button>

</body>
</template>

<style>
body{
background-color: blanchedalmond;
max-width: 600px;
margin: auto;
}
</style>
