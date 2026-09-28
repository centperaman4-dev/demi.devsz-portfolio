<script setup>
import { X, ExternalLink, Github, Layers, Database, CheckCircle, Sparkles } from 'lucide-vue-next'

const props = defineProps({
  project: {
    type: Object,
    default: null
  }
})

const emit = defineEmits(['close'])
</script>

<template>
  <div 
    v-if="project" 
    class="fixed inset-0 z-50 flex items-center justify-center p-4 sm:p-6 overflow-y-auto bg-black/80 backdrop-blur-md animate-fadeIn"
    @click.self="emit('close')"
  >
    <div class="relative w-full max-w-3xl max-h-[90vh] overflow-y-auto rounded-2xl border border-violet-500/30 bg-[#0f0b1a] p-6 sm:p-8 text-slate-200 shadow-2xl shadow-violet-950/60">
      
      <!-- Modal Header -->
      <div class="flex items-start justify-between border-b border-white/10 pb-4 mb-6">
        <div>
          <span class="inline-flex items-center gap-1.5 rounded-full bg-violet-500/10 px-3 py-1 text-xs font-semibold text-violet-400 border border-violet-500/20 mb-2">
            <Sparkles :size="13" />
            {{ project.category || 'Academic & Web Project' }}
          </span>
          <h2 class="text-2xl sm:text-3xl font-bold text-white tracking-tight">
            {{ project.title }}
          </h2>
        </div>

        <button 
          @click="emit('close')"
          class="rounded-lg p-1.5 text-gray-400 transition hover:bg-white/10 hover:text-white"
          aria-label="Close modal"
        >
          <X :size="22" />
        </button>
      </div>

      <!-- Preview Image -->
      <div class="relative overflow-hidden rounded-xl border border-white/10 bg-slate-900 mb-6 aspect-video">
        <img 
          :src="project.image" 
          :alt="project.title" 
          class="h-full w-full object-cover object-top transition duration-500 hover:scale-105"
        />
      </div>

      <!-- Main Modal Content -->
      <div class="space-y-6 text-left">
        <!-- Overview / Problem Statement -->
        <div>
          <h3 class="text-sm font-bold uppercase tracking-wider text-violet-400 mb-2">
            Project Overview & Objective
          </h3>
          <p class="text-sm sm:text-base text-gray-300 leading-relaxed">
            {{ project.longDescription || project.description }}
          </p>
        </div>

        <!-- System Architecture & Design Highlights (BSIT focus) -->
        <div v-if="project.architecture" class="rounded-xl border border-violet-500/20 bg-violet-500/5 p-4 space-y-2">
          <h3 class="flex items-center gap-2 text-sm font-bold uppercase tracking-wider text-violet-300">
            <Database :size="16" /> System Architecture & Technical Highlights
          </h3>
          <p class="text-xs sm:text-sm text-gray-300 leading-relaxed">
            {{ project.architecture }}
          </p>
        </div>

        <!-- Key Features List -->
        <div v-if="project.features && project.features.length">
          <h3 class="text-sm font-bold uppercase tracking-wider text-violet-400 mb-3">
            Core Features & Modules
          </h3>
          <ul class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
            <li 
              v-for="(feature, idx) in project.features" 
              :key="idx"
              class="flex items-start gap-2 text-xs sm:text-sm text-gray-300"
            >
              <CheckCircle :size="16" class="text-violet-400 shrink-0 mt-0.5" />
              <span>{{ feature }}</span>
            </li>
          </ul>
        </div>

        <!-- Tech Stack Used -->
        <div>
          <h3 class="text-sm font-bold uppercase tracking-wider text-violet-400 mb-2">
            Technologies & Tools
          </h3>
          <div class="flex flex-wrap gap-2">
            <span 
              v-for="tech in project.technologies" 
              :key="tech"
              class="rounded-lg bg-white/5 border border-white/10 px-3 py-1 text-xs font-medium text-violet-300"
            >
              {{ tech }}
            </span>
          </div>
        </div>

        <!-- Action Links -->
        <div class="flex flex-wrap items-center gap-4 border-t border-white/10 pt-6 mt-6">
          <a
            v-if="project.demo && project.demo !== '#'"
            :href="project.demo"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-2 rounded-xl bg-violet-600 px-5 py-2.5 text-sm font-semibold text-white transition hover:bg-violet-500 shadow-lg shadow-violet-600/30"
          >
            <ExternalLink :size="16" />
            Launch Live Demo
          </a>

          <a
            v-if="project.github && project.github !== '#'"
            :href="project.github"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-5 py-2.5 text-sm font-semibold text-gray-200 transition hover:border-violet-500 hover:text-violet-400"
          >
            <Github :size="16" />
            View Source Code
          </a>

          <button
            @click="emit('close')"
            class="ml-auto rounded-xl px-4 py-2.5 text-sm font-medium text-gray-400 hover:text-white"
          >
            Close
          </button>
        </div>

      </div>

    </div>
  </div>
</template>

<style scoped>
@keyframes fadeIn {
  from { opacity: 0; transform: scale(0.97); }
  to { opacity: 1; transform: scale(1); }
}
.animate-fadeIn {
  animation: fadeIn 0.2s ease-out forwards;
}
</style>
