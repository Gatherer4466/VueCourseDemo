<script setup lang="ts">
import { ref } from 'vue'

const count = ref(0)

function incrementCount() {
  count.value++
}
</script>

<template>
  <!-- make this button work -->
  <div>
    <button @click="incrementCount">Count is: {{ count }}</button>
  </div>
</template>
