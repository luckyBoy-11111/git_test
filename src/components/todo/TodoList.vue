<template>
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
</template>

<script setup lang="ts">
import TodoItem from './TodoItem.vue'
import type { TodoItemType } from '../../types/todo'

defineProps<{
  items: TodoItemType[]
}>()

defineEmits<{
  toggle: [id: string]
  remove: [id: string]
}>()
</script>

<style scoped>
.todo-list {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
