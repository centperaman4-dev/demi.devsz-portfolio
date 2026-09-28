<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { 
  ArrowRight, 
  FileText, 
  Figma, 
  Sparkles, 
  Layout, 
  MousePointer2, 
  Layers, 
  Eye, 
  Palette, 
  ChevronDown 
} from 'lucide-vue-next'

const emit = defineEmits(['openResume'])

// Dynamic UI/UX Role Switcher
const roles = [
  "BSIT 3rd-Year UI/UX Student",
  "Product & Interaction Designer",
  "Design Systems & Figma Prototyper",
  "User Research & Usability Enthusiast"
]
const currentRoleIndex = ref(0)
let roleInterval = null

onMounted(() => {
  roleInterval = setInterval(() => {
    currentRoleIndex.value = (currentRoleIndex.value + 1) % roles.length
  }, 2800)
})

onUnmounted(() => {
  if (roleInterval) clearInterval(roleInterval)
})
</script>

<template>
  <section
    id="home"
    class="relative min-h-screen flex flex-col justify-center items-center px-6 pt-28 pb-16 overflow-hidden bg-designer-grid"
  >
    <!-- Ambient Blue Glow Blobs -->
    <div class="pointer-events-none absolute -top-20 left-1/2 -translate-x-1/2 h-[420px] w-[700px] rounded-full bg-gradient-to-tr from-blue-600/20 via-sky-500/20 to-cyan-400/15 blur-[130px]"></div>
    <div class="pointer-events-none absolute bottom-12 right-12 h-72 w-72 rounded-full bg-blue-600/15 blur-[110px]"></div>

    <div class="relative z-10 mx-auto grid max-w-7xl items-center gap-12 lg:grid-cols-12 w-full">
      
      <!-- Left Column: Hero Text Content -->
      <div class="text-center lg:text-left lg:col-span-7 space-y-6">
        
        <!-- Status Pill -->
        <div class="inline-flex items-center gap-2 rounded-full border border-blue-500/30 bg-blue-950/50 px-4 py-1.5 backdrop-blur-md shadow-sm">
          <span class="flex h-2 w-2 relative">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-blue-400 opacity-75"></span>
            <span class="relative inline-flex rounded-full h-2 w-2 bg-blue-500"></span>
          </span>
          <span class="text-xs font-semibold uppercase tracking-wider text-blue-300">
            Open for UI/UX Internship / OJT & Capstone Design
          </span>
        </div>

        <!-- Main Headline -->
        <div class="space-y-2">
          <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
            Crafting Human-Centered Digital Products
          </p>
          <h1 class="text-4xl sm:text-6xl lg:text-7xl font-black text-white tracking-tight leading-[1.1]">
            Vinz <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 via-sky-400 to-cyan-300">Design</span>
          </h1>
          
          <!-- Animated Role Badge -->
          <div class="h-10 flex items-center justify-center lg:justify-start">
            <span class="font-mono text-base sm:text-xl md:text-2xl font-semibold text-blue-300 flex items-center gap-2">
              <span class="text-sky-400 font-bold">✦</span>
              <transition name="fade-slide" mode="out-in">
                <span :key="currentRoleIndex" class="inline-block">{{ roles[currentRoleIndex] }}</span>
              </transition>
            </span>
          </div>
        </div>

        <!-- Bio Paragraph -->
        <p class="mx-auto lg:mx-0 max-w-2xl text-base sm:text-lg text-slate-300 leading-relaxed font-normal">
          3rd-year Bachelor of Science in Information Technology student focusing entirely on <strong>UI/UX Design</strong>. I transform complex user problems into intuitive mobile and web interfaces through user research, wireframing, interactive Figma prototypes, and scalable design systems.
        </p>

        <!-- CTA Action Buttons -->
        <div class="flex flex-wrap items-center justify-center lg:justify-start gap-4 pt-2">
          <a
            href="#casestudies"
            class="inline-flex items-center gap-2 rounded-xl bg-blue-600 hover:bg-blue-500 text-white px-6 py-3.5 text-sm font-bold shadow-lg shadow-blue-600/30 transition hover:scale-[1.02] active:scale-[0.98]"
          >
            <span>Explore Case Studies</span>
            <ArrowRight :size="16" />
          </a>

          <button
            @click="emit('openResume')"
            class="inline-flex items-center gap-2 rounded-xl border border-blue-500/30 bg-blue-950/40 px-6 py-3.5 text-sm font-bold text-blue-200 shadow-sm transition hover:bg-blue-600/20 hover:border-blue-400 hover:scale-[1.02] active:scale-[0.98] cursor-pointer"
          >
            <FileText :size="16" />
            <span>UX Resume / CV</span>
          </button>

          <a
            href="#playground"
            class="inline-flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-5 py-3.5 text-sm font-semibold text-slate-300 transition hover:bg-white/10 hover:text-white"
          >
            <Sparkles :size="15" />
            <span>UX Lab</span>
          </a>
        </div>

        <!-- Quick Design Tools Tags -->
        <div class="flex items-center justify-center lg:justify-start gap-3 pt-3 text-xs text-gray-400 font-mono">
          <span class="uppercase tracking-wider text-gray-500">Primary Tools:</span>
          <span class="rounded bg-blue-500/10 px-2 py-0.5 text-blue-300 border border-blue-500/20">Figma</span>
          <span class="rounded bg-blue-500/10 px-2 py-0.5 text-blue-300 border border-blue-500/20">FigJam</span>
          <span class="rounded bg-blue-500/10 px-2 py-0.5 text-blue-300 border border-blue-500/20">Tailwind UI</span>
          <span class="rounded bg-blue-500/10 px-2 py-0.5 text-blue-300 border border-blue-500/20">Miro</span>
        </div>

      </div>

      <!-- Right Column: Avatar with Floating Design Badges -->
      <div class="flex justify-center lg:col-span-5 relative">
        
        <!-- Glowing Ring Container -->
        <div class="relative flex items-center justify-center">
          
          <!-- Ambient Backlight -->
          <div class="absolute inset-0 rounded-full bg-gradient-to-tr from-blue-600 to-cyan-500 opacity-40 blur-2xl animate-pulse-glow"></div>

          <!-- Main Avatar Outer Ring -->
          <div class="relative h-72 w-72 sm:h-88 sm:w-88 md:h-96 md:w-96 rounded-full p-2 bg-gradient-to-b from-blue-500/50 via-sky-500/20 to-transparent shadow-2xl">
            <div class="h-full w-full rounded-full overflow-hidden border-2 border-blue-400/40 bg-[#0f172a] relative group">
              <img
                src="/profile.jpg"
                alt="Vinz UI/UX Designer Avatar"
                class="h-full w-full object-cover object-center transition duration-700 group-hover:scale-105"
              />
            </div>
          </div>

          <!-- Floating Badge 1: Figma & Auto-Layout -->
          <div class="absolute -top-2 -left-4 sm:left-0 rounded-xl glass-card px-3.5 py-2 flex items-center gap-2.5 shadow-xl animate-float">
            <div class="flex h-7 w-7 items-center justify-center rounded-lg bg-blue-500/20 text-blue-400 font-bold text-xs">
              <Figma :size="15" />
            </div>
            <div class="text-left font-sans">
              <p class="text-[11px] font-bold text-white">Auto-Layout & Variants</p>
              <p class="text-[9px] text-gray-400">Design Systems</p>
            </div>
          </div>

          <!-- Floating Badge 2: User Research & Heuristics -->
          <div class="absolute -bottom-2 -left-2 sm:left-4 rounded-xl glass-card px-3.5 py-2 flex items-center gap-2.5 shadow-xl animate-float-delayed">
            <div class="flex h-7 w-7 items-center justify-center rounded-lg bg-cyan-500/20 text-cyan-400">
              <Eye :size="15" />
            </div>
            <div class="text-left font-sans">
              <p class="text-[11px] font-bold text-white">Heuristic Evaluation</p>
              <p class="text-[9px] text-gray-400">Usability Testing</p>
            </div>
          </div>

          <!-- Floating Badge 3: BSIT 3rd Year UI/UX -->
          <div class="absolute top-1/3 -right-6 sm:-right-4 rounded-xl glass-card px-3.5 py-2 flex items-center gap-2.5 shadow-xl animate-float">
            <div class="flex h-7 w-7 items-center justify-center rounded-lg bg-blue-600 text-white shadow-sm">
              <Palette :size="15" />
            </div>
            <div class="text-left font-sans">
              <p class="text-[11px] font-bold text-white">BSIT 3rd Year</p>
              <p class="text-[9px] text-blue-300">UX Specialization</p>
            </div>
          </div>

        </div>

      </div>

    </div>

    <!-- Quick Metrics & Design Stats Bar -->
    <div class="relative z-10 mx-auto max-w-5xl w-full mt-16 pt-8 border-t border-white/10">
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
        
        <div class="glass-card rounded-2xl p-4 sm:p-5">
          <p class="text-2xl sm:text-3xl font-extrabold text-blue-400 font-mono">3rd Year</p>
          <p class="text-xs sm:text-sm text-gray-400 font-medium mt-1">BSIT Standing</p>
        </div>

        <div class="glass-card rounded-2xl p-4 sm:p-5">
          <p class="text-2xl sm:text-3xl font-extrabold text-sky-400 font-mono">6+</p>
          <p class="text-xs sm:text-sm text-gray-400 font-medium mt-1">UI/UX Case Studies</p>
        </div>

        <div class="glass-card rounded-2xl p-4 sm:p-5">
          <p class="text-2xl sm:text-3xl font-extrabold text-cyan-400 font-mono">100+</p>
          <p class="text-xs sm:text-sm text-gray-400 font-medium mt-1">Figma Components</p>
        </div>

        <div class="glass-card rounded-2xl p-4 sm:p-5">
          <p class="text-2xl sm:text-3xl font-extrabold text-emerald-400 font-mono">100%</p>
          <p class="text-xs sm:text-sm text-gray-400 font-medium mt-1">User-Centered Focus</p>
        </div>

      </div>
    </div>

    <!-- Scroll Down Prompt -->
    <a href="#about" class="mt-8 text-gray-500 hover:text-blue-400 transition animate-bounce" aria-label="Scroll to About">
      <ChevronDown :size="24" />
    </a>

  </section>
</template>

<style scoped>
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.25s ease;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(8px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>