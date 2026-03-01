<template>
  <header class="todo-header">
    <span class="todo-header-prefix">&gt;</span>
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
  position: relative;
}

.todo-header-prefix {
  position: absolute;
  left: 0;
  top: 0.15em;
  font-family: var(--tg-font-mono);
  font-size: 1.5rem;
  color: var(--tg-accent);
  text-shadow: 0 0 8px var(--tg-glow);
  animation: blink 1.2s step-end infinite;
}

@keyframes blink {
  50% { opacity: 0.4; }
}

.todo-title {
  margin: 0 0 0 1.5rem;
  padding-left: 0.25rem;
  font-family: var(--tg-font-display);
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: var(--tg-text);
  text-transform: uppercase;
  text-shadow: 0 0 20px rgba(0, 212, 255, 0.2);
}

.todo-subtitle {
  margin: 0.35rem 0 0 1.5rem;
  padding-left: 0.25rem;
  font-family: var(--tg-font-mono);
  font-size: 0.8rem;
  color: var(--tg-text-muted);
  letter-spacing: 0.02em;
}
</style>
