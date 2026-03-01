<template>
  <div ref="listWrapRef" class="todo-list-wrap">
    <ul class="todo-list">
      <TodoItem
        v-for="item in items"
        :key="item.id"
        :text="item.text"
        :done="item.done"
        @toggle="$emit('toggle', item.id)"
        @remove="$emit('remove', item.id)"
      />
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
import type { TodoItemType } from '../../types/todo'

defineProps<{
  items: TodoItemType[]
}>()

defineEmits<{
  toggle: [id: string]
  remove: [id: string]
}>()

const listWrapRef = ref<HTMLElement | null>(null)

function scrollToBottom() {
  if (listWrapRef.value) {
    listWrapRef.value.scrollTop = listWrapRef.value.scrollHeight
  }
}

defineExpose({ scrollToBottom })
</script>

<style scoped>
.todo-list-wrap {
  height: 300px;
  overflow-y: auto;
  overflow-x: hidden;
  border: 1px solid var(--tg-border);
  border-radius: 2px;
  background: var(--tg-bg-input);
}

/* 滚动条 - 与页面科技风格一致 */
.todo-list-wrap::-webkit-scrollbar {
  width: 8px;
}

.todo-list-wrap::-webkit-scrollbar-track {
  background: rgba(0, 212, 255, 0.06);
  border-radius: 4px;
  border-left: 1px solid var(--tg-border);
}

.todo-list-wrap::-webkit-scrollbar-thumb {
  background: var(--tg-border);
  border-radius: 4px;
}

.todo-list-wrap::-webkit-scrollbar-thumb:hover {
  background: var(--tg-accent-dim);
  box-shadow: 0 0 6px var(--tg-glow);
}

.todo-list-wrap::-webkit-scrollbar-thumb:active {
  background: var(--tg-accent);
  box-shadow: 0 0 8px var(--tg-glow);
}

/* Firefox 滚动条 */
.todo-list-wrap {
  scrollbar-width: thin;
  scrollbar-color: var(--tg-border) rgba(0, 212, 255, 0.06);
}

.todo-list {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
