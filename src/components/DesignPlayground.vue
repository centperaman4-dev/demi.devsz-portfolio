<script setup>
import { ref, computed } from 'vue'
import { 
  Sparkles, 
  Palette, 
  MousePointer2, 
  CheckCircle2, 
  Check, 
  Heart, 
  Bookmark, 
  Layers, 
  Sliders, 
  Eye, 
  ThumbsUp,
  RefreshCw
} from 'lucide-vue-next'

const emit = defineEmits(['showToast'])

const activeTab = ref('interactions')

// Lab 1: Micro-interactions state
const isLiked = ref(false)
const isBookmarked = ref(false)
const activePill = ref('Design')

const handleRipple = (e) => {
  const rect = e.currentTarget.getBoundingClientRect()
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top
  emit('showToast', `Micro-interaction triggered at (${Math.round(x)}px, ${Math.round(y)}px)`)
}

// Lab 2: Color Palette & Accessibility Contrast Checker
const colorSwatches = [
  { name: 'Royal Blue (Primary)', hex: '#2563eb', bgClass: 'bg-blue-600', textLight: true, hexClean: '2563eb' },
  { name: 'Electric Sky (Accent)', hex: '#38bdf8', bgClass: 'bg-sky-400', textLight: false, hexClean: '38bdf8' },
  { name: 'Deep Navy (Dark BG)', hex: '#0b1120', bgClass: 'bg-[#0b1120]', textLight: true, hexClean: '0b1120' },
  { name: 'Crisp White (Light BG)', hex: '#ffffff', bgClass: 'bg-white', textLight: false, hexClean: 'ffffff' },
  { name: 'Cyan Glow (Highlight)', hex: '#06b6d4', bgClass: 'bg-cyan-500', textLight: true, hexClean: '06b6d4' },
]

const selectedBg = ref(colorSwatches[2]) // Deep Navy
const selectedFg = ref(colorSwatches[3]) // White

// Helper to compute contrast ratio
const getLuminance = (hex) => {
  const rgb = hex.replace('#', '').match(/.{2}/g).map(x => parseInt(x, 16) / 255)
  const a = rgb.map(v => v <= 0.03928 ? v / 12.92 : Math.pow((v + 0.055) / 1.055, 2.4))
  return a[0] * 0.2126 + a[1] * 0.7152 + a[2] * 0.0722
}

const contrastRatio = computed(() => {
  const lum1 = getLuminance(selectedBg.value.hex)
  const lum2 = getLuminance(selectedFg.value.hex)
  const brightest = Math.max(lum1, lum2)
  const darkest = Math.min(lum1, lum2)
  const ratio = (brightest + 0.05) / (darkest + 0.05)
  return ratio.toFixed(2)
})

const isWcagPass = computed(() => parseFloat(contrastRatio.value) >= 4.5)

// Lab 3: A/B Usability Simulator
const votesA = ref(18)
const votesB = ref(34)
const hasVoted = ref(false)

const vote = (variant) => {
  if (variant === 'A') votesA.value++
  if (variant === 'B') votesB.value++
  hasVoted.value = true
  emit('showToast', `Recorded vote for Variant ${variant}!`)
}

const resetVotes = () => {
  votesA.value = 18
  votesB.value = 34
  hasVoted.value = false
}
</script>

<template>
  <section id="playground" class="px-6 py-24 relative bg-[#0c1324]">
    <div class="mx-auto max-w-6xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-14">
        <div class="inline-flex items-center gap-2 rounded-full border border-blue-500/30 bg-blue-950/40 px-3.5 py-1 text-xs font-semibold text-blue-300 mb-3">
          <Sparkles :size="14" />
          <span>Classroom Interactive Presentation Lab</span>
        </div>
        <h2 class="text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          Interactive UI/UX Lab
        </h2>
        <p class="mt-4 text-base text-gray-400">
          A live sandbox demonstrating micro-interactions, color accessibility ratios, and A/B usability heuristics.
        </p>
      </div>

      <!-- Lab Mode Switcher -->
      <div class="flex flex-wrap items-center justify-center gap-2 mb-10">
        <button
          @click="activeTab = 'interactions'"
          class="flex items-center gap-2 rounded-2xl px-5 py-2.5 text-xs sm:text-sm font-semibold transition cursor-pointer"
          :class="[
            activeTab === 'interactions'
              ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/30'
              : 'glass-card text-gray-300 hover:text-white'
          ]"
        >
          <MousePointer2 :size="16" />
          <span>Micro-Interactions</span>
        </button>

        <button
          @click="activeTab = 'contrast'"
          class="flex items-center gap-2 rounded-2xl px-5 py-2.5 text-xs sm:text-sm font-semibold transition cursor-pointer"
          :class="[
            activeTab === 'contrast'
              ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/30'
              : 'glass-card text-gray-300 hover:text-white'
          ]"
        >
          <Palette :size="16" />
          <span>WCAG Contrast Inspector</span>
        </button>

        <button
          @click="activeTab = 'abtesting'"
          class="flex items-center gap-2 rounded-2xl px-5 py-2.5 text-xs sm:text-sm font-semibold transition cursor-pointer"
          :class="[
            activeTab === 'abtesting'
              ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/30'
              : 'glass-card text-gray-300 hover:text-white'
          ]"
        >
          <Sliders :size="16" />
          <span>A/B Usability Simulator</span>
        </button>
      </div>

      <!-- Lab Panel 1: Micro-Interactions -->
      <div v-if="activeTab === 'interactions'" class="glass-card rounded-3xl p-6 sm:p-10 border border-blue-900/40 text-left space-y-8 animate-fadeIn">
        <div>
          <h3 class="text-xl font-bold text-white">
            1. Tactile Micro-Interactions & State Design
          </h3>
          <p class="text-xs sm:text-sm text-gray-400 mt-1">
            Test these buttons to experience elastic feedback, ripple states, and toggle states.
          </p>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          
          <!-- Interaction 1: Spring Bounce Button -->
          <div class="rounded-2xl border border-white/10 bg-white/[0.02] p-5 flex flex-col items-center justify-center gap-4 text-center">
            <span class="text-xs font-mono font-semibold text-gray-400">Elastic Magnetic Spring</span>
            <button
              @click="handleRipple"
              class="rounded-xl bg-blue-600 hover:bg-blue-500 active:scale-90 transition-transform duration-200 px-6 py-3 text-xs font-bold text-white shadow-lg shadow-blue-600/30 cursor-pointer"
            >
              Click For Spring Bounce
            </button>
            <span class="text-[10px] text-blue-400">active:scale-90 + spring transition</span>
          </div>

          <!-- Interaction 2: Interactive Heart / Bookmark Toggle -->
          <div class="rounded-2xl border border-white/10 bg-white/[0.02] p-5 flex flex-col items-center justify-center gap-4 text-center">
            <span class="text-xs font-mono font-semibold text-gray-400">State Persistence Toggles</span>
            <div class="flex items-center gap-4">
              <button
                @click="isLiked = !isLiked"
                class="p-3 rounded-2xl border transition-all cursor-pointer"
                :class="isLiked ? 'bg-rose-500 text-white border-rose-600 scale-110 shadow-lg shadow-rose-500/30' : 'bg-white/5 border-white/10 text-slate-400'"
                title="Like button"
              >
                <Heart :size="20" :class="{ 'fill-current': isLiked }" />
              </button>

              <button
                @click="isBookmarked = !isBookmarked"
                class="p-3 rounded-2xl border transition-all cursor-pointer"
                :class="isBookmarked ? 'bg-blue-600 text-white border-blue-700 scale-110 shadow-lg shadow-blue-600/30' : 'bg-white/5 border-white/10 text-slate-400'"
                title="Bookmark button"
              >
                <Bookmark :size="20" :class="{ 'fill-current': isBookmarked }" />
              </button>
            </div>
            <span class="text-[10px] text-blue-400">Visual feedback with instant state change</span>
          </div>

          <!-- Interaction 3: Segmented Pill Switcher -->
          <div class="rounded-2xl border border-white/10 bg-white/[0.02] p-5 flex flex-col items-center justify-center gap-4 text-center sm:col-span-2 lg:col-span-1">
            <span class="text-xs font-mono font-semibold text-gray-400">Segmented Control</span>
            <div class="flex p-1 rounded-xl bg-white/5 border border-white/10 w-full max-w-xs">
              <button
                v-for="pill in ['UX', 'UI', 'HCI']"
                :key="pill"
                @click="activePill = pill"
                class="flex-1 py-1.5 text-xs font-bold rounded-lg transition-all cursor-pointer"
                :class="activePill === pill ? 'bg-blue-600 text-white shadow-md' : 'text-gray-400 hover:text-white'"
              >
                {{ pill }}
              </button>
            </div>
            <span class="text-[10px] text-blue-400">Active pill: {{ activePill }} selected</span>
          </div>

        </div>
      </div>

      <!-- Lab Panel 2: WCAG Color Contrast Inspector -->
      <div v-if="activeTab === 'contrast'" class="glass-card rounded-3xl p-6 sm:p-10 border border-blue-900/40 text-left space-y-8 animate-fadeIn">
        <div>
          <h3 class="text-xl font-bold text-white">
            2. Live WCAG 2.1 AA/AAA Contrast Ratio Calculator
          </h3>
          <p class="text-xs sm:text-sm text-gray-400 mt-1">
            Click a background and text swatch to compute the real-time mathematical contrast score.
          </p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center">
          
          <!-- Swatches Selection -->
          <div class="lg:col-span-7 space-y-5">
            <!-- Background Selector -->
            <div>
              <p class="text-xs font-bold uppercase tracking-wider text-gray-400 mb-2">1. Choose Background Color:</p>
              <div class="flex flex-wrap gap-2">
                <button
                  v-for="swatch in colorSwatches"
                  :key="swatch.hex"
                  @click="selectedBg = swatch"
                  class="flex items-center gap-2 px-3 py-1.5 rounded-xl border text-xs font-semibold transition cursor-pointer"
                  :class="selectedBg.hex === swatch.hex ? 'border-blue-500 ring-2 ring-blue-500/40 bg-blue-950/40' : 'border-white/10 bg-white/5'"
                >
                  <span class="h-4 w-4 rounded-full border border-black/20 inline-block" :class="swatch.bgClass"></span>
                  <span class="text-gray-200">{{ swatch.name }}</span>
                </button>
              </div>
            </div>

            <!-- Foreground Selector -->
            <div>
              <p class="text-xs font-bold uppercase tracking-wider text-gray-400 mb-2">2. Choose Foreground (Text) Color:</p>
              <div class="flex flex-wrap gap-2">
                <button
                  v-for="swatch in colorSwatches"
                  :key="'fg-' + swatch.hex"
                  @click="selectedFg = swatch"
                  class="flex items-center gap-2 px-3 py-1.5 rounded-xl border text-xs font-semibold transition cursor-pointer"
                  :class="selectedFg.hex === swatch.hex ? 'border-blue-500 ring-2 ring-blue-500/40 bg-blue-950/40' : 'border-white/10 bg-white/5'"
                >
                  <span class="h-4 w-4 rounded-full border border-black/20 inline-block" :class="swatch.bgClass"></span>
                  <span class="text-gray-200">{{ swatch.name }}</span>
                </button>
              </div>
            </div>
          </div>

          <!-- Live Computed Preview Card -->
          <div class="lg:col-span-5">
            <div 
              class="rounded-3xl p-6 transition-all duration-200 border border-black/20 shadow-xl space-y-4"
              :style="{ backgroundColor: selectedBg.hex, color: selectedFg.hex }"
            >
              <div class="flex items-center justify-between">
                <span class="text-xs font-mono uppercase tracking-wider opacity-80">Live Sample Text</span>
                <span 
                  class="rounded-full px-2.5 py-0.5 text-[10px] font-bold font-mono uppercase"
                  :class="isWcagPass ? 'bg-emerald-500 text-white' : 'bg-rose-500 text-white'"
                >
                  {{ isWcagPass ? 'PASS WCAG AA' : 'FAIL CONTRAST' }}
                </span>
              </div>

              <div>
                <p class="text-3xl font-black font-mono tracking-tight">{{ contrastRatio }}:1</p>
                <p class="text-xs opacity-90 mt-1">
                  {{ isWcagPass ? 'Excellent contrast (minimum 4.5:1 required for normal body text).' : 'Insufficient contrast. May cause strain for visually impaired users.' }}
                </p>
              </div>

              <div class="pt-3 border-t border-current/20 text-xs">
                <p class="font-bold">Sample Heading 18px</p>
                <p class="text-xs opacity-80 mt-1">This is how body text will render against this background.</p>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- Lab Panel 3: A/B Usability Simulator -->
      <div v-if="activeTab === 'abtesting'" class="glass-card rounded-3xl p-6 sm:p-10 border border-blue-900/40 text-left space-y-8 animate-fadeIn">
        <div class="flex items-start justify-between">
          <div>
            <h3 class="text-xl font-bold text-white">
              3. Classroom A/B Usability Experiment
            </h3>
            <p class="text-xs sm:text-sm text-gray-400 mt-1">
              Test your classmates: Which Call-To-Action button creates clearer visual affordance?
            </p>
          </div>

          <button
            @click="resetVotes"
            class="flex items-center gap-1.5 text-xs text-blue-400 hover:underline cursor-pointer"
          >
            <RefreshCw :size="12" />
            <span>Reset Poll</span>
          </button>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          
          <!-- Variant A -->
          <div class="rounded-3xl border border-white/10 bg-white/[0.02] p-6 space-y-5 text-center">
            <span class="text-xs font-mono font-bold text-slate-400 uppercase">Variant A (Flat Minimalist)</span>
            <div class="h-24 flex items-center justify-center">
              <button
                @click="vote('A')"
                class="rounded-lg border border-slate-700 bg-slate-800 text-white px-5 py-2.5 text-xs font-semibold hover:bg-slate-700 transition cursor-pointer"
              >
                Enroll in Course
              </button>
            </div>
            <div class="pt-3 border-t border-white/5 flex items-center justify-between text-xs">
              <span class="text-slate-400">Votes: <strong class="text-white">{{ votesA }}</strong></span>
              <button 
                @click="vote('A')"
                class="text-blue-400 font-bold hover:underline cursor-pointer"
              >
                + Vote Variant A
              </button>
            </div>
          </div>

          <!-- Variant B -->
          <div class="rounded-3xl border border-blue-500/40 bg-blue-950/20 p-6 space-y-5 text-center relative overflow-hidden">
            <span class="text-xs font-mono font-bold text-blue-400 uppercase">Variant B (High Affordance + Icon)</span>
            <div class="h-24 flex items-center justify-center">
              <button
                @click="vote('B')"
                class="rounded-xl bg-blue-600 hover:bg-blue-500 text-white px-6 py-3 text-xs font-bold shadow-lg shadow-blue-600/30 hover:scale-105 transition duration-200 flex items-center gap-2 cursor-pointer"
              >
                <span>Enroll in Course</span>
                <Sparkles :size="14" />
              </button>
            </div>
            <div class="pt-3 border-t border-white/10 flex items-center justify-between text-xs">
              <span class="text-gray-400">Votes: <strong class="text-blue-400 font-bold">{{ votesB }}</strong></span>
              <button 
                @click="vote('B')"
                class="text-blue-400 font-bold hover:underline cursor-pointer"
              >
                + Vote Variant B (Leading 🏆)
              </button>
            </div>
          </div>

        </div>

        <!-- UX Insight Callout -->
        <div class="rounded-2xl bg-blue-950/40 border border-blue-900/40 p-4 text-xs text-gray-300">
          💡 <strong>UX Takeaway for Class:</strong> Variant B achieves higher click-through rates because elevation, electric blue contrast, and directional cues offer higher visual affordance according to Fitts's Law.
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(6px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fadeIn {
  animation: fadeIn 0.25s ease-out forwards;
}
</style>
