<template>
  <div class="progress-bar" ref="progressBar" @click="changePosition($event.offsetX)">
    <div
      class="current-progress"
      :style="`width:${props.progress}%`"
      @drag="changePosition($event.offsetX)"
    ></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps<{
  progress: number
}>()

const emit = defineEmits<{
  change: [percentage: number]
}>()

const progressBar = ref<HTMLDivElement>()

const changePosition = (offsetX: number) => {
  const div = progressBar.value
  let total = 100
  if (div) total = div.offsetWidth

  const result = percentage(offsetX, total)
  emit('change', result)
}

const percentage = (partialValue: number, totalValue: number) => (100 * partialValue) / totalValue
</script>

<style scoped>
.progress-bar {
  color: #000 !important;
  background-color: #ffffff29 !important;
  border-radius: 3px;
}

.current-progress {
  color: #000 !important;
  background-color: #9e9e9e !important;
  height: 6px;
  border-radius: 3px;
}
</style>
