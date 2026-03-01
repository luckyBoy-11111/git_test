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
      {{ done ? '✓' : '' }}
    </span>
    <span class="todo-text" :title="text">{{ text }}</span>
    <button
      type="button"
      class="todo-remove-btn"
      aria-label="删除"
      @click="emit('remove')"
    >
      ×
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
  cursor: pointer;
  user-select: none;
}

.todo-checkbox:hover {
  border-color: #7aa2f7;
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
  min-width: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.todo-remove-btn {
  flex-shrink: 0;
  width: 1.5rem;
  height: 1.5rem;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.25rem;
  line-height: 1;
  color: #565f89;
  background: transparent;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.todo-remove-btn:hover {
  color: #f7768e;
  background: rgba(247, 118, 142, 0.15);
}
</style>
