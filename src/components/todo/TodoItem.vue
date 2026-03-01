<template>
  <li class="todo-item" :class="{ 'todo-item--done': done }">
    <span
      class="todo-checkbox"
      role="button"
      tabindex="0"
      aria-label="切换完成状态"
      @click="emit('toggle')"
      @keydown.enter.prevent="emit('toggle')"
      @keydown.space.prevent="emit('toggle')"
    >
      <span v-if="done" class="todo-checkbox-check">✓</span>
    </span>
    <span class="todo-text">{{ text }}</span>
    <button
      type="button"
      class="todo-remove-btn"
      aria-label="删除"
      @click="emit('remove')"
    >
      <span class="todo-remove-icon">×</span>
    </button>
  </li>
</template>

<script setup lang="ts">
defineProps<{
  text: string
  done?: boolean
}>()

const emit = defineEmits<{
  toggle: []
  remove: []
}>()
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.7rem 0;
  border-bottom: 1px solid var(--tg-border);
  color: var(--tg-text);
  font-family: var(--tg-font-mono);
  font-size: 0.9rem;
  letter-spacing: 0.02em;
  transition: background 0.15s;
}

.todo-item:hover {
  background: rgba(0, 212, 255, 0.03);
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-checkbox {
  flex-shrink: 0;
  width: 1.15rem;
  height: 1.15rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid var(--tg-border);
  border-radius: 2px;
  cursor: pointer;
  user-select: none;
  transition: border-color 0.2s, box-shadow 0.2s, background 0.2s;
}

.todo-checkbox:hover {
  border-color: var(--tg-accent);
  box-shadow: 0 0 8px var(--tg-glow);
}

.todo-checkbox-check {
  font-size: 0.7rem;
  color: var(--tg-done);
  text-shadow: 0 0 6px var(--tg-done-glow);
}

.todo-item--done .todo-checkbox {
  background: rgba(0, 255, 136, 0.12);
  border-color: var(--tg-done);
  box-shadow: 0 0 10px var(--tg-done-glow);
}

.todo-item--done .todo-text {
  text-decoration: line-through;
  color: var(--tg-text-muted);
}

.todo-text {
  flex: 1;
}

.todo-remove-btn {
  flex-shrink: 0;
  width: 1.6rem;
  height: 1.6rem;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  line-height: 1;
  color: var(--tg-text-muted);
  background: transparent;
  border: 1px solid transparent;
  border-radius: 2px;
  cursor: pointer;
  transition: color 0.2s, background 0.2s, border-color 0.2s, box-shadow 0.2s;
}

.todo-remove-btn:hover {
  color: var(--tg-danger);
  background: var(--tg-danger-glow);
  border-color: rgba(255, 51, 102, 0.3);
  box-shadow: 0 0 12px var(--tg-danger-glow);
}

.todo-remove-icon {
  font-weight: 300;
  line-height: 1;
}
</style>
