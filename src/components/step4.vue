<script setup lang="ts">
import { ref } from 'vue'

const text = ref('')
</script>

<template>
  <div>
    <input v-model="text" placeholder="Type here" />
    <p>{{ text }}</p>
  </div>
</template>
