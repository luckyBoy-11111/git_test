<template>
  <ul class="todo-list">
    <TodoItem
      v-for="item in items"
      :key="item.id"
      :text="item.text"
      :done="item.done"
    />
  </ul>
</template>

<script setup lang="ts">
import TodoItem from './TodoItem.vue'
import type { TodoItemType } from '../../types/todo'

defineProps<{
  items: TodoItemType[]
}>()
</script>

<style scoped>
.todo-list {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
