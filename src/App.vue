<script setup>
import {ref} from 'vue'

let todos = ref([])
let NewTodos = ref('')

function AddTodo () {
  todos.value.push(NewTodos.value)

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
<li v-for="(todo, index) in todos"><button @click="DeleteTodos">🚮</button>{{ todo }}</li>
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
