<template>
  <div class="todo-page">
    <div class="todo-page-bg" aria-hidden="true" />
    <div class="todo-card">
      <div class="todo-card-glow" aria-hidden="true" />
      <div class="todo-layout">
        <aside class="todo-side-add">
          <TodoHeader />
          <TodoInput @add="addTodo" />
        </aside>
        <main class="todo-side-list">
          <TodoList
            ref="todoListRef"
            :items="todoItems"
            @toggle="toggleTodo"
            @remove="openDeleteConfirm"
          />
          <TodoFooter :total="todoItems.length" :done-count="doneCount" />
        </main>
      </div>
    </div>

    <ConfirmDialog
      :visible="pendingDeleteId !== null"
      title="确认删除456"
      :message="deleteConfirmMessage"
      confirm-text="确定删除"
      cancel-text="取消"
      @confirm="confirmDelete"
      @cancel="pendingDeleteId = null"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, nextTick } from 'vue'
import TodoHeader from './components/todo/TodoHeader.vue'
import TodoInput from './components/todo/TodoInput.vue'
import TodoList from './components/todo/TodoList.vue'
import TodoFooter from './components/todo/TodoFooter.vue'
import ConfirmDialog from './components/common/ConfirmDialog.vue'
import type { TodoItemType } from './types/todo'

const pendingDeleteId = ref<string | null>(null)
const todoListRef = ref<{ scrollToBottom: () => void } | null>(null)

const deleteConfirmMessage = computed(() => {
  if (!pendingDeleteId.value) return '确定要删除该任务吗？'
  const item = todoItems.value.find((i: TodoItemType) => i.id === pendingDeleteId.value)
  return item ? `确定要删除「${item.text}」吗？此操作不可恢复。` : '确定要删除该任务吗？'
})

const todoItems = ref<TodoItemType[]>([
  { id: '1', text: '完成项目文档', done: true },
  { id: '2', text: '代码评审', done: false },
  { id: '3', text: '准备周会汇报', done: false },
  { id: '4', text: '更新依赖版本', done: true },
  { id: '5', text: '编写单元测试', done: false },
])

const doneCount = computed(() =>
  todoItems.value.filter((item: TodoItemType) => item.done).length
)

function generateId(): string {
  return Date.now().toString(36) + Math.random().toString(36).slice(2)
}

async function addTodo(text: string) {
  const trimmed = text.trim()
  if (!trimmed) return
  todoItems.value.push({
    id: generateId(),
    text: trimmed,
    done: false,
  })
  await nextTick()
  todoListRef.value?.scrollToBottom()
}

function toggleTodo(id: string) {
  const item = todoItems.value.find((i: TodoItemType) => i.id === id)
  if (item) item.done = !item.done
}

function openDeleteConfirm(id: string) {
  pendingDeleteId.value = id
}

function confirmDelete() {
  if (pendingDeleteId.value) {
    removeTodo(pendingDeleteId.value)
    pendingDeleteId.value = null
  }
}

function removeTodo(id: string) {
  todoItems.value = todoItems.value.filter((item: TodoItemType) => item.id !== id)
}
</script>

<style scoped>
.todo-page {
  position: relative;
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 2rem 1rem;
  overflow: hidden;
}

/* 科技感网格背景 */
.todo-page-bg {
  position: fixed;
  inset: 0;
  background:
    linear-gradient(180deg, transparent 0%, rgba(0, 212, 255, 0.03) 50%, transparent 100%),
    linear-gradient(90deg, rgba(0, 212, 255, 0.04) 1px, transparent 1px),
    linear-gradient(rgba(0, 212, 255, 0.04) 1px, transparent 1px);
  background-size: 100% 100%, 60px 60px, 60px 60px;
  background-position: 0 0, 0 0, 0 0;
  pointer-events: none;
}

.todo-card {
  position: relative;
  width: 100%;
  max-width: 720px;
  background: var(--tg-bg-card);
  border: 1px solid var(--tg-border);
  border-radius: 4px;
  padding: 1.75rem;
  backdrop-filter: blur(12px);
  box-shadow:
    0 0 0 1px rgba(0, 212, 255, 0.08),
    0 24px 48px rgba(0, 0, 0, 0.4);
}

.todo-layout {
  display: flex;
  gap: 2rem;
  align-items: flex-start;
}

.todo-side-add {
  flex-shrink: 0;
  width: 220px;
  padding-right: 1rem;
  border-right: 1px solid var(--tg-border);
}

.todo-side-list {
  flex: 1;
  min-width: 0;
}

.todo-side-add :deep(.todo-input-area) {
  flex-direction: column;
  margin-bottom: 0;
}
.todo-side-add :deep(.todo-input) {
  width: 100%;
  box-sizing: border-box;
}

.todo-card-glow {
  position: absolute;
  top: -50%;
  left: 50%;
  transform: translateX(-50%);
  width: 80%;
  height: 100%;
  background: radial-gradient(ellipse, var(--tg-glow) 0%, transparent 70%);
  opacity: 0.15;
  pointer-events: none;
}
</style>
