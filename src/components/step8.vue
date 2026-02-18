<script setup lang="ts">
import { ref, onMounted } from 'vue'

const pElementRef = ref<HTMLParagraphElement | null>(null)

onMounted(() => {
  if (pElementRef.value) {
    pElementRef.value.textContent =
      'This is the Night Mail crossing the border Bringing the cheque and the postal order'
  }
})
</script>

<template>
  <div>
    <p ref="pElementRef">Hello</p>
  </div>
</template>
