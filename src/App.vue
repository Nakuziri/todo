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
<h1>My Todo Application</h1>

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
<ul>
<li v-for="(todo, index) in todos.filter(todoFilter)" :class= "{completed: todo.complete}">
  <input class="checkbox" type="checkbox" v-model="todo.complete" >
  {{ todo.text }}
  <button @click="DeleteTodos(index)">🚮</button>
</li>
</ul>




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
}

li:hover > button {
  display:flex;
}
button {text-align: right;
}

</style>
