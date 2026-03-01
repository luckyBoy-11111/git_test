<template>
  <Teleport to="body">
    <Transition name="confirm-fade">
      <div
        v-if="visible"
        class="confirm-overlay"
        role="dialog"
        aria-modal="true"
        aria-labelledby="confirm-title"
        @click.self="handleCancel"
      >
        <div class="confirm-dialog">
          <h2 id="confirm-title" class="confirm-title">{{ title }}</h2>
          <p class="confirm-message">{{ message }}</p>
          <div class="confirm-actions">
            <button
              type="button"
              class="confirm-btn confirm-btn--cancel"
              @click="handleCancel"
            >
              {{ cancelText }}
            </button>
            <button
              type="button"
              class="confirm-btn confirm-btn--danger"
              @click="handleConfirm"
            >
              {{ confirmText }}
            </button>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup lang="ts">
import { watch } from 'vue'

const props = withDefaults(
  defineProps<{
    visible: boolean
    title?: string
    message?: string
    confirmText?: string
    cancelText?: string
  }>(),
  {
    title: '确认删除',
    message: '确定要删除该任务吗？',
    confirmText: '确定删除',
    cancelText: '取消',
  }
)

const emit = defineEmits<{
  confirm: []
  cancel: []
}>()

function handleConfirm() {
  emit('confirm')
}

function handleCancel() {
  emit('cancel')
}

function onKeydown(e: KeyboardEvent) {
  if (e.key === 'Escape') handleCancel()
}

watch(
  () => props.visible,
  (visible) => {
    if (visible) {
      document.addEventListener('keydown', onKeydown)
    } else {
      document.removeEventListener('keydown', onKeydown)
    }
  }
)
</script>

<style scoped>
.confirm-overlay {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  background: rgba(6, 10, 15, 0.75);
  backdrop-filter: blur(4px);
  z-index: 1000;
}

.confirm-dialog {
  width: 100%;
  max-width: 360px;
  padding: 1.5rem;
  background: var(--tg-bg-card);
  border: 1px solid var(--tg-border);
  border-radius: 4px;
  box-shadow:
    0 0 0 1px rgba(0, 212, 255, 0.1),
    0 24px 48px rgba(0, 0, 0, 0.5);
}

.confirm-title {
  margin: 0 0 0.75rem;
  font-family: var(--tg-font-display);
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--tg-text);
  letter-spacing: 0.05em;
}

.confirm-message {
  margin: 0 0 1.5rem;
  font-family: var(--tg-font-mono);
  font-size: 0.9rem;
  color: var(--tg-text-muted);
  line-height: 1.5;
}

.confirm-actions {
  display: flex;
  gap: 0.75rem;
  justify-content: flex-end;
}

.confirm-btn {
  padding: 0.5rem 1.25rem;
  font-family: var(--tg-font-mono);
  font-size: 0.9rem;
  font-weight: 500;
  border-radius: 2px;
  border: 1px solid transparent;
  cursor: pointer;
  transition: box-shadow 0.2s, opacity 0.2s;
}

.confirm-btn--cancel {
  color: var(--tg-text);
  background: var(--tg-bg-input);
  border-color: var(--tg-border);
}

.confirm-btn--cancel:hover {
  border-color: var(--tg-accent);
  box-shadow: 0 0 12px var(--tg-glow);
}

.confirm-btn--danger {
  color: #0a0a0a;
  background: var(--tg-danger);
  border-color: var(--tg-danger);
}

.confirm-btn--danger:hover {
  box-shadow: 0 0 16px var(--tg-danger-glow);
}

/* 过渡动画 */
.confirm-fade-enter-active,
.confirm-fade-leave-active {
  transition: opacity 0.2s ease;
}

.confirm-fade-enter-active .confirm-dialog,
.confirm-fade-leave-active .confirm-dialog {
  transition: transform 0.2s ease;
}

.confirm-fade-enter-from,
.confirm-fade-leave-to {
  opacity: 0;
}

.confirm-fade-enter-from .confirm-dialog,
.confirm-fade-leave-to .confirm-dialog {
  transform: scale(0.95);
}
</style>
