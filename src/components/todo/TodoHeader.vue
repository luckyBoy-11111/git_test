<template>
  <header class="todo-header">
    <h1 class="todo-title">{{ title }}</h1>
    <p v-if="subtitle" class="todo-subtitle">{{ subtitle }}</p>
  </header>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    title?: string
    subtitle?: string
  }>(),
  {
    title: 'To-Do List',
    subtitle: '记录待办事项',
  }
)
</script>

<style scoped>
.todo-header {
  margin-bottom: 1.5rem;
}

.todo-title {
  margin: 0 0 0.25rem;
  font-size: 1.75rem;
  font-weight: 600;
  color: #c0caf5;
  letter-spacing: -0.02em;
}

.todo-subtitle {
  margin: 0;
  font-size: 0.9rem;
  color: #565f89;
}
</style>
