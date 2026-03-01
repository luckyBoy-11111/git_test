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
  border-top: 1px solid var(--tg-border);
  font-family: var(--tg-font-mono);
  font-size: 0.8rem;
  color: var(--tg-text-muted);
  letter-spacing: 0.04em;
}

.todo-count {
  display: block;
}
.todo-count::before {
  content: '// ';
  color: var(--tg-accent);
  opacity: 0.7;
}
</style>
