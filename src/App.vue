<script setup>
import {ref} from 'vue'

let todos = ref(['A', 'B', 'C'])
let newTodo = ref('')
function a() {
  todos.value.push(input.value)
  input.value = ''
}

function deleteTodo(index) {
  todos.value.splice(index, 1)
}
</script>

<template>
  <h1>My Todo Application</h1>
  <ol>
<li v-for="(todo, index) in todos">
  <button>💀</button>
  {{ index }}
  {{ todo }}
</li>
  </ol>

  <input v-model="(newTodo)" @keydown.enter="addTodo" >
  <button @click="newTodo">Add Todo</button>

</template>

<style>
</style>