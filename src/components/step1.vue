<script setup lang="ts">
import { reactive } from 'vue'

// component logic
// declare some reactive state here.
const counter = reactive({
  count: 0,
})

function countUp() {
  counter.count++
}
</script>

<template>
  <div>
    <h1>Make me {{ counter.count }}</h1>
    <button :onclick="countUp">click me for reactivity</button>
  </div>
</template>
