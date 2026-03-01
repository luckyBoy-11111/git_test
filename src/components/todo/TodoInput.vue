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
      <span class="todo-add-btn-text">{{ buttonText }}</span>
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
  padding: 0.6rem 1rem;
  font-family: var(--tg-font-mono);
  font-size: 0.9rem;
  color: var(--tg-text);
  background: var(--tg-bg-input);
  border: 1px solid var(--tg-border);
  border-radius: 2px;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.todo-input::placeholder {
  color: var(--tg-text-dim);
}

.todo-input:hover {
  border-color: rgba(0, 212, 255, 0.35);
}

.todo-input:focus {
  border-color: var(--tg-border-focus);
  box-shadow: 0 0 0 2px var(--tg-glow);
}

.todo-add-btn {
  padding: 0.6rem 1.2rem;
  font-family: var(--tg-font-mono);
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--tg-bg-deep);
  background: var(--tg-accent);
  border: 1px solid var(--tg-accent);
  border-radius: 2px;
  cursor: pointer;
  transition: box-shadow 0.2s, transform 0.15s;
}

.todo-add-btn:hover {
  box-shadow: 0 0 16px var(--tg-glow), 0 0 32px rgba(0, 212, 255, 0.2);
}

.todo-add-btn:active {
  transform: scale(0.98);
}

.todo-add-btn-text {
  position: relative;
  z-index: 1;
}
</style>
