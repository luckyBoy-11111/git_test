<template>
  <div class="todo-page">
    <div class="todo-card">
      <TodoHeader />
      <TodoInput />
      <TodoList :items="todoItems" />
      <TodoFooter :total="todoItems.length" :done-count="doneCount" />
    </div>
  </div>
</template>

<script setup lang="ts">
import TodoHeader from './components/todo/TodoHeader.vue'
import TodoInput from './components/todo/TodoInput.vue'
import TodoList from './components/todo/TodoList.vue'
import TodoFooter from './components/todo/TodoFooter.vue'
import type { TodoItemType } from './types/todo'

// 静态数据，后续可改为 ref/reactive 并接入增删改逻辑
const todoItems: TodoItemType[] = [
  { id: '1', text: '完成项目文档', done: true },
  { id: '2', text: '代码评审', done: false },
  { id: '3', text: '准备周会汇报', done: false },
  { id: '4', text: '更新依赖版本', done: true },
  { id: '5', text: '编写单元测试', done: false },
]

const doneCount = todoItems.filter((item) => item.done).length
</script>

<style scoped>
.todo-page {
  min-height: 100vh;
  padding: 2rem 1rem;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  background: linear-gradient(160deg, #1a1b26 0%, #24283b 100%);
}

.todo-card {
  width: 100%;
  max-width: 420px;
  background: #2d2e3e;
  border-radius: 12px;
  padding: 1.75rem;
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.35);
}
</style>
