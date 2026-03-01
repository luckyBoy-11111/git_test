<template>
  <div class="todo-input-area">
    <input
      ref="inputRef"
      v-model="inputValue"
      type="text"
      class="todo-input"
      :placeholder="placeholder"
      @keydown.enter="handleAdd"
    />
    <button type="button" class="todo-add-btn" @click="handleAdd">
      {{ buttonText }}
    </button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

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

const emit = defineEmits<{
  add: [text: string]
}>()

const inputValue = ref('')
const inputRef = ref<HTMLInputElement | null>(null)

function handleAdd() {
  const text = inputValue.value.trim()
  if (!text) return
  emit('add', text)
  inputValue.value = ''
  inputRef.value?.focus()
}
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
  cursor: pointer;
}

.todo-add-btn:hover {
  background: #6a92e7;
}
</style>
