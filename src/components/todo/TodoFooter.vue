<template>
  <div class="todo-footer">
    <span class="todo-count">{{ displayText }}</span>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = withDefaults(
  defineProps<{
    total?: number
    doneCount?: number
    summaryText?: string
  }>(),
  {
    total: 0,
    doneCount: 0,
    summaryText: '',
  }
)

const displayText = computed(() => {
  if (props.summaryText) return props.summaryText
  return `共 ${props.total} 项，已完成 ${props.doneCount} 项`
})
</script>

<style scoped>
.todo-footer {
  margin-top: 1.25rem;
  padding-top: 1rem;
  border-top: 1px solid #363b54;
  font-size: 0.85rem;
  color: #565f89;
}

.todo-count {
  display: block;
}
</style>
