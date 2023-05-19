<script setup>
import { ref, watch } from 'vue'
let filter = ref('all')
let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
let newTodo = ref('')
let input = ref('')

function addTodo() {
  todos.value.push({
    text: newTodo.value,
    complete: false
  })
  newTodo.value = ''
}

function deleteTodo(index) {
  todos.value.splice(index, 1)
}

watch(todos, function (value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, { deep: true })

function todoFilter(todo) {
  if (filter.value == 'active') {
    return todo.complete == false
  } else if (filter.value == 'complete'){
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
  <h1>My Todo Application</h1>
  <p v-if="todos.length > 0">
  </p>
  <p> {{ todos.filter(activeFilter).length}} items left</p>
  <p>
  <input name="filter" type="radio" value="all" v-model="filter">
  <label>All</label>
  <input name="filter" type="radio" value="active" v-model="filter">
  <label>Active</label>
  <input name="filter" type="radio" value="complete" v-model="filter">
  <label>Complete</label>
  </p>
  <input v-model="newTodo" @keydown.enter="addTodo">
  <button @click="addTodo">Add Todo</button>
  <div v-for="(todo, index) in todos.filter(todoFilter)" :class="{ completed: todo.complete }">
    <input type="checkbox" v-model="todo.complete">
    <button @click="deleteTodo">💀</button>

    {{ index }}
    {{ todo.text }}
  </div>
</template>

<style>
body {
  background: rgb(131,58,180);
background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);

  font-family: Arial, Helvetica, sans-serif;

  text-align: center;

  color: black
}

.complete {
  text-decoration: line-through;
  color: #c2c2cc;
}
input[type="checkbox"]::before {
  /* ...existing styles */

  transform-origin: bottom left;
  clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
  border-radius: 12px;
  padding: 15px, 12px;
  margin: 5px;

    background-color: rgb(239, 137, 96);
    border-radius: 12px;
    color:whitesmoke;
    padding: 8px 12px 10px 18px;
    /* border: 2px red solid; */
    border-width: 0 0 5px 0;
    border-color:indianred
  
}
</style>