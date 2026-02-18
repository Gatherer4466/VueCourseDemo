<script setup lang="ts">
import { ref } from 'vue'
import ChildComp from './ChildComponents/Step13Child.vue'

const msg = ref('from parent')
</script>

<template>
  <div>
    <ChildComp>Message to child: {{ msg }}</ChildComp>
  </div>
</template>
