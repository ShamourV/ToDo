<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos'))??[])
let newTodo = ref('')
let input = ref('')

function addTodo () {
  todos.value.push({
   text:newTodo.value,
   complete: false
    })
    newTodo.value=''
  }

function deleteTodo(index) {
  todos.value.splice(index, 1)
}

watch(todos, function(value) {
window.localStorage.setItem('todos',JSON.stringify(value))
}, {deep: true})
</script>



<template>
  <h1>My Todo Application</h1>
<div v-for="(todo, index) in todos" :class="{completed: todo.complete}">
  <input type="checkbox" v-model="todo.complete">
  <button @click="deleteTodo">💀</button>
  {{ index }}
  {{ todo.text }}
</div>
  <input v-model="newTodo" @keydown.enter="addTodo">
  <button @click="addTodo">Add Todo</button>
</template>




<style>
body{
  background: rgb(131,58,180);
background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);
}
body{
  text-align: center;
}
body{
color: indianred;
} 
.complete {
  text-decoration: line-through;
  color: #c2c2cc;
}
input[type="checkbox"]::before {
  /* ...existing styles */

  transform-origin: bottom left;
  clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
}
</style>