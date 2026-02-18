<script setup lang="ts">
import { ref } from 'vue'
import Step12Child from './ChildComponents/Step12Child.vue'

const childMsg = ref('No child msg yet')
</script>

<template>
  <div>
    <Step12Child @response="(msg) => (childMsg = msg)" />
    <p>{{ childMsg }}</p>
  </div>
</template>
