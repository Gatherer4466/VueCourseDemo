<script setup lang="ts">
import { ref } from 'vue'

// give each todo a unique id
let id = 0

const newTodo = ref('')
type todo = { id: number; text: string }

const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' },
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo: todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <div>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" required placeholder="new todo" />
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.text }}
        <button @click="removeTodo(todo)">X</button>
      </li>
    </ul>
  </div>
</template>
