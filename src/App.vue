<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
let NewTodos = ref('')
let input = ref ('')

watch(todos, function(value) {
  window.localStorage.setItem('todos',JSON.stringify(value))
}, {deep: true})

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
  <input class="checkbox" type="checkbox" v-model="todo.complete">
  <button @click="DeleteTodos(index)">🚮</button>
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
.checkbox:hover{
color: blueviolet;
}
</style>
