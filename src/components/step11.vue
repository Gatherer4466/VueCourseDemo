<script setup lang="ts">
import { ref } from 'vue'
import Step11Child from './ChildComponents/Step11Child.vue'

const greeting = ref('Hello from parent')
</script>

<template>
  <Step11Child :msg="greeting" />
</template>
