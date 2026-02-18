<script setup lang="ts">
import { ref } from 'vue'

const titleClass = ref('title')
</script>

<template>
  <div>
    <h1 :class="titleClass">Make me red</h1>
    <!-- add dynamic class binding here -->
  </div>
</template>

<style>
.title {
  color: red;
}
</style>
