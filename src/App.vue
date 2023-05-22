<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
let NewTodos = ref('')
let input = ref ('')
let filter = ref('all')

watch(todos, function(value) {
  window.localStorage.setItem('todos',JSON.stringify(value))
}, {deep: true})


function AddTodo () { 

  if (NewTodos.value != '') {
    todos.value.push({
    text: NewTodos.value,
    complete: false
  })
  NewTodos.value = ''
  } 
}


function DeleteTodos (index) {
    todos.value.splice(index, 1)
  }


function todoFilter (todo) {
  if (filter.value == 'active') {
    return todo.complete == false
  } else if (filter.value == 'complete') {
    return todo.complete == true
  } else {
    return true
  }
  
}

function activeFilter (todo) {
  return todo.complete == false
}

</script>


<template>

  <body>

<h1>My To-do Application</h1>

<p v-if="todos.length > 0">
 <input name="filter" type="radio" value="all" v-model="filter">
 <label>All</label>

 <input name="filter" type="radio" value="active" v-model="filter">
 <label>Active</label>

 <input name="filter" type="radio" value="complete" v-model="filter">
 <label>Complete</label>
</p>

<p>{{ todos.filter(activeFilter).length }} items left</p>
<input id="todoInput" v-model="NewTodos" placeholder="Press enter to add todo" @keydown.enter="AddTodo">

<div>
<li v-for="(todo, index) in todos.filter(todoFilter)" :class= "{completed: todo.complete}">
  <input id="check" type="checkbox" v-model="todo.complete" >
  {{ todo.text }}
  <button id="button" @click="DeleteTodos(index)">🚮</button>
</li>
</div>

</body>
</template>





<style>
.completed {
  text-decoration: line-through;
  color: #E7CBCB;
}

body{
background-color: #99627A;
max-width: 800px;
margin: auto;
text-align: center;
padding: 0;
margin: 0;
color: white;

}

li {
  background-color: #643843;
  padding: 15px;
  border-radius: 20px;
  margin: 5px;
  text-align: left;
}

#todoInput {
 padding: 15px;
 border-radius: 20px;
 background-color: #643843;
 color: white;
}

#button {
  text-align: right;
  height: 25px;
  width: 35px;
}

input[type='checkbox']{
  appearance: none;
  -webkit-appearance: none;
  height: 23px;
  width: 23px;
  background-color: #d5d5d5;
  border-radius: 5px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  outline: none;
}

input[type='checkbox']:after{
  font-family: "Font Awesome 5 Free";
  font-weight:600;
  content: "\f00c";
  font-size: 15px;
  color: white;
  display: none;
}

input[type='checkbox']:hover{
  background-color: #a5a5a5;
}

input[type='checkbox']:checked{
  background-color: #E7CBCB;
}

input[type='checkbox']:checked:after{
  display: block;
}

</style>
