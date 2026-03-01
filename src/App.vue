<template>
  <div class="todo-page">
    <div class="todo-card">
      <h1 class="todo-title">To-Do List</h1>
      <p class="todo-subtitle">记录待办事项</p>

      <div class="todo-input-area">
        <input
          type="text"
          class="todo-input"
          placeholder="添加新任务..."
          readonly
        />
        <button type="button" class="todo-add-btn">添加</button>
      </div>

      <ul class="todo-list">
        <li class="todo-item todo-item--done">
          <span class="todo-checkbox" aria-hidden="true">✓</span>
          <span class="todo-text">完成项目文档</span>
        </li>
        <li class="todo-item">
          <span class="todo-checkbox" aria-hidden="true"></span>
          <span class="todo-text">代码评审</span>
        </li>
        <li class="todo-item">
          <span class="todo-checkbox" aria-hidden="true"></span>
          <span class="todo-text">准备周会汇报</span>
        </li>
        <li class="todo-item todo-item--done">
          <span class="todo-checkbox" aria-hidden="true">✓</span>
          <span class="todo-text">更新依赖版本</span>
        </li>
        <li class="todo-item">
          <span class="todo-checkbox" aria-hidden="true"></span>
          <span class="todo-text">编写单元测试</span>
        </li>
      </ul>

      <div class="todo-footer">
        <span class="todo-count">共 5 项，已完成 2 项</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// 静态页面，无逻辑
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

.todo-title {
  margin: 0 0 0.25rem;
  font-size: 1.75rem;
  font-weight: 600;
  color: #c0caf5;
  letter-spacing: -0.02em;
}

.todo-subtitle {
  margin: 0 0 1.5rem;
  font-size: 0.9rem;
  color: #565f89;
}

.todo-input-area {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.todo-input {
  flex: 1;
  padding: 0.65rem 1rem;
  font-size: 0.95rem;
  color: #c0caf5;
  background: #1f2335;
  border: 1px solid #3b4261;
  border-radius: 8px;
  outline: none;
}

.todo-input::placeholder {
  color: #565f89;
}

.todo-add-btn {
  padding: 0.65rem 1.25rem;
  font-size: 0.95rem;
  font-weight: 500;
  color: #c0caf5;
  background: #7aa2f7;
  border: none;
  border-radius: 8px;
  cursor: default;
}

.todo-list {
  list-style: none;
  margin: 0;
  padding: 0;
}

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

.todo-footer {
  margin-top: 1.25rem;
  padding-top: 1rem;
  border-top: 1px solid #363b54;
  font-size: 0.85rem;
  color: #565f89;
}

.todo-count {
  display: block;
}
</style>
