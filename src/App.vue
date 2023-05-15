<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
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
<div v-for="(todo, index) in todos">
  <input type="checkbox" v-model="todo.complete">
  <button @click="deleteTodo">💀</button>
  {{ todo.text }}
</div>
  <input v-model="newTodo" @keydown.enter="addTodo">
  <button @click="addTodo">Add Todo</button>
</template>




<style>

</style>