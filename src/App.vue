<script setup lang="ts">
import { ref, computed } from 'vue'
import type { Component } from 'vue'
import CodeViewer from './components/CodeViewer.vue'

interface Step {
  component: Component
  fullCode: string
}

const componentModules = import.meta.glob('./components/step*.vue', {
  eager: true,
})

const rawModules = import.meta.glob('./components/step*.vue', {
  eager: true,
  as: 'raw',
})

function extractStepNumber(path: string): number {
  const match = path.match(/step(\d+)\.vue$/)
  return match ? parseInt(match[1]!, 10) : 0
}

const steps: Step[] = Object.keys(componentModules)
  .sort((a, b) => extractStepNumber(a) - extractStepNumber(b))
  .map((path) => ({
    component: (componentModules[path] as any).default,
    fullCode: rawModules[path] as string,
  }))

const currentStep = ref(0)
const showCode = ref(false)

const currentStepData = computed(() => steps[currentStep.value])
const currentComponent = computed(() => currentStepData.value!.component)

function nextStep() {
  if (currentStep.value < steps.length - 1) {
    currentStep.value++
    showCode.value = false
  }
}

function prevStep() {
  if (currentStep.value > 0) {
    currentStep.value--
    showCode.value = false
  }
}
</script>

<template>
  <div class="container py-5">
    <h2 class="text-center mb-4 fw-bold">Vue Tutorial Explorer</h2>

    <div class="d-flex justify-content-center gap-2 mb-4 flex-wrap">
      <button
        v-for="(_, index) in steps"
        :key="index"
        class="btn"
        :class="index === currentStep ? 'btn-primary' : 'btn-outline-primary'"
        @click="((currentStep = index), (showCode = false))"
      >
        Step {{ index + 1 }}
      </button>
    </div>

    <div class="progress mb-4" style="height: 6px">
      <div
        class="progress-bar"
        :style="{ width: ((currentStep + 1) / steps.length) * 100 + '%' }"
      />
    </div>

    <div class="card shadow-sm">
      <div class="card-body">
        <div class="mb-4">
          <component :is="currentComponent" />
        </div>

        <hr />

        <div class="d-flex justify-content-end mb-2">
          <button class="btn btn-sm btn-outline-dark" @click="showCode = !showCode">
            {{ showCode ? 'Hide Code' : 'Show Code' }}
          </button>
        </div>

        <CodeViewer v-if="showCode" :code="currentStepData!.fullCode" />

        <div class="d-flex justify-content-between mt-4">
          <button class="btn btn-outline-secondary" @click="prevStep" :disabled="currentStep === 0">
            Previous
          </button>

          <button
            class="btn btn-primary"
            @click="nextStep"
            :disabled="currentStep === steps.length - 1"
          >
            Next
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
