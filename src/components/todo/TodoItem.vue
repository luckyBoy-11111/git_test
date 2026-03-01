<template>
  <li class="todo-item" :class="{ 'todo-item--done': done }">
    <span class="todo-checkbox" aria-hidden="true">{{ done ? '✓' : '' }}</span>
    <span class="todo-text">{{ text }}</span>
  </li>
</template>

<script setup lang="ts">
defineProps<{
  text: string
  done?: boolean
}>()
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 0;
  border-bottom: 1px solid #363b54;
  color: #a9b1d6;
  font-size: 0.95rem;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-checkbox {
  flex-shrink: 0;
  width: 1.25rem;
  height: 1.25rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid #565f89;
  border-radius: 4px;
  font-size: 0.75rem;
  color: #7aa2f7;
}

.todo-item--done .todo-checkbox {
  background: #7aa2f7;
  border-color: #7aa2f7;
}

.todo-item--done .todo-text {
  text-decoration: line-through;
  color: #565f89;
}

.todo-text {
  flex: 1;
}
</style>
