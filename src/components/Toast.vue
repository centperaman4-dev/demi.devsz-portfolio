<script setup>
import { Sparkles } from 'lucide-vue-next'

defineProps({
  message: {
    type: String,
    default: ''
  },
  visible: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <transition name="toast-slide">
    <div
      v-if="visible"
      class="fixed bottom-6 right-6 z-50 flex items-center gap-3 rounded-2xl border border-blue-500/40 bg-[#0c152a]/95 px-5 py-3.5 text-sm font-semibold text-white shadow-2xl shadow-blue-950/40 backdrop-blur-xl"
    >
      <div class="flex h-7 w-7 items-center justify-center rounded-lg bg-blue-500/20 text-blue-300">
        <Sparkles :size="16" />
      </div>
      <span>{{ message }}</span>
    </div>
  </transition>
</template>

<style scoped>
.toast-slide-enter-active,
.toast-slide-leave-active {
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

.toast-slide-enter-from {
  opacity: 0;
  transform: translateY(16px) scale(0.96);
}

.toast-slide-leave-to {
  opacity: 0;
  transform: translateY(8px) scale(0.96);
}
</style>
