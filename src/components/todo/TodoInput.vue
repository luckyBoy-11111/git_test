<template>
  <div class="todo-input-area">
    <input
      type="text"
      class="todo-input"
      :placeholder="placeholder"
      readonly
    />
    <button type="button" class="todo-add-btn">{{ buttonText }}</button>
  </div>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    placeholder?: string
    buttonText?: string
  }>(),
  {
    placeholder: '添加新任务...',
    buttonText: '添加',
  }
)
</script>

<style scoped>
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
</style>
