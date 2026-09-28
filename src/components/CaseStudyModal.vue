<script setup>
import { 
  X, 
  ExternalLink, 
  Figma, 
  Sparkles, 
  Eye, 
  CheckCircle, 
  Users, 
  Layers, 
  Palette,
  Target,
  FileText
} from 'lucide-vue-next'

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
    class="fixed inset-0 z-50 flex items-center justify-center p-4 sm:p-6 overflow-y-auto bg-black/85 backdrop-blur-md animate-fadeIn"
    @click.self="emit('close')"
  >
    <div class="relative w-full max-w-4xl max-h-[92vh] overflow-y-auto rounded-3xl border border-blue-900/60 bg-[#0f172a] p-6 sm:p-9 text-slate-200 shadow-2xl shadow-blue-950/40 text-left">
      
      <!-- Modal Header -->
      <div class="flex items-start justify-between border-b border-white/10 pb-5 mb-6">
        <div>
          <span class="inline-flex items-center gap-1.5 rounded-full bg-blue-950/60 px-3.5 py-1 text-xs font-semibold text-blue-400 border border-blue-800 mb-2">
            <Sparkles :size="13" />
            {{ project.badge }}
          </span>
          <h2 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
            {{ project.title }}
          </h2>
          <p class="text-xs sm:text-sm text-gray-400 mt-1">
            {{ project.role }} • {{ project.timeline }}
          </p>
        </div>

        <button 
          @click="emit('close')"
          class="rounded-xl p-2 text-slate-400 hover:bg-white/10 hover:text-white transition"
          aria-label="Close modal"
        >
          <X :size="22" />
        </button>
      </div>

      <!-- Preview Image Showcase -->
      <div class="relative overflow-hidden rounded-2xl border border-white/10 bg-slate-900 mb-7 aspect-video shadow-md">
        <img 
          :src="project.image" 
          :alt="project.title" 
          class="h-full w-full object-cover object-top transition duration-500 hover:scale-105"
        />
      </div>

      <!-- Main Case Study Content Body -->
      <div class="space-y-7">
        
        <!-- Problem & Solution Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
          <div class="rounded-2xl bg-rose-950/20 border border-rose-900/40 p-4 sm:p-5">
            <h3 class="text-xs font-bold uppercase tracking-wider text-rose-400 mb-2 flex items-center gap-1.5">
              <span>🚨 The User Problem</span>
            </h3>
            <p class="text-xs sm:text-sm text-gray-300 leading-relaxed">
              {{ project.problem }}
            </p>
          </div>

          <div class="rounded-2xl bg-emerald-950/20 border border-emerald-900/40 p-4 sm:p-5">
            <h3 class="text-xs font-bold uppercase tracking-wider text-emerald-400 mb-2 flex items-center gap-1.5">
              <span>✨ The UX Solution</span>
            </h3>
            <p class="text-xs sm:text-sm text-gray-300 leading-relaxed">
              {{ project.solution }}
            </p>
          </div>
        </div>

        <!-- Target Persona & Research Insights -->
        <div class="rounded-2xl bg-blue-950/30 border border-blue-900/40 p-5 space-y-3">
          <h3 class="flex items-center gap-2 text-sm font-bold uppercase tracking-wider text-blue-300">
            <Users :size="16" /> User Persona & Research Key Takeaways
          </h3>
          <p class="text-xs sm:text-sm text-gray-300 leading-relaxed">
            <strong>Target Audience:</strong> {{ project.persona }}
          </p>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 pt-1">
            <div 
              v-for="(insight, idx) in project.insights" 
              :key="idx"
              class="flex items-start gap-2 text-xs text-gray-300 bg-white/[0.03] p-2.5 rounded-xl border border-white/5"
            >
              <CheckCircle :size="15" class="text-blue-400 shrink-0 mt-0.5" />
              <span>{{ insight }}</span>
            </div>
          </div>
        </div>

        <!-- UI & Design System Highlights -->
        <div>
          <h3 class="text-xs font-bold uppercase tracking-wider text-blue-400 mb-3">
            Figma Design Decisions & Features
          </h3>
          <ul class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <li 
              v-for="(feature, idx) in project.features" 
              :key="idx"
              class="flex items-start gap-2.5 text-xs sm:text-sm text-gray-300"
            >
              <CheckCircle :size="16" class="text-blue-400 shrink-0 mt-0.5" />
              <span>{{ feature }}</span>
            </li>
          </ul>
        </div>

        <!-- Design Tags & Tools -->
        <div>
          <h3 class="text-xs font-bold uppercase tracking-wider text-blue-400 mb-2">
            Design Tools & Methodologies Used
          </h3>
          <div class="flex flex-wrap gap-2">
            <span 
              v-for="tech in project.technologies" 
              :key="tech"
              class="rounded-lg bg-white/5 border border-white/10 px-3 py-1 text-xs font-medium text-blue-300 font-mono"
            >
              {{ tech }}
            </span>
          </div>
        </div>

        <!-- Action Links -->
        <div class="flex flex-wrap items-center gap-4 border-t border-white/10 pt-6 mt-6">
          <a
            :href="project.figmaLink || '#'"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-2 rounded-xl bg-blue-600 hover:bg-blue-500 text-white px-5 py-2.5 text-sm font-bold shadow-md shadow-blue-600/30 transition hover:scale-[1.02]"
          >
            <Figma :size="16" />
            <span>Open Figma File / Preview</span>
          </a>

          <button
            @click="emit('close')"
            class="ml-auto rounded-xl px-4 py-2.5 text-sm font-medium text-gray-400 hover:text-white"
          >
            Close Case Study
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
