<script setup>
import { ref, computed } from 'vue'
import { 
  Figma, 
  Palette, 
  Eye, 
  Layout, 
  Sparkles, 
  Search, 
  Layers, 
  BookOpen,
  MousePointer2,
  CheckCircle2,
  Sliders
} from 'lucide-vue-next'

const selectedCategory = ref('all')

const categories = [
  { id: 'all', label: 'All Design Skills', icon: Sparkles },
  { id: 'tools', label: 'Design Tools', icon: Figma },
  { id: 'ux', label: 'UX Research & Strategy', icon: Search },
  { id: 'ui', label: 'UI & Visual Craft', icon: Palette },
  { id: 'prototyping', label: 'UI Prototyping', icon: Layout },
  { id: 'hci', label: 'HCI & Usability Laws', icon: BookOpen },
]

const skillItems = [
  // Design Tools
  { name: 'Figma (Expert)', category: 'tools', level: 'Advanced', desc: 'Auto-layout, dynamic components, nested variants, smart animate, design tokens' },
  { name: 'FigJam & Miro', category: 'tools', level: 'Advanced', desc: 'User flows, brainstorming, crazy 8s, empathy maps, affinity diagrams' },
  { name: 'Adobe XD', category: 'tools', level: 'Proficient', desc: 'Artboards, wireframing, transitions, voice prototyping' },
  { name: 'Adobe Illustrator', category: 'tools', level: 'Intermediate', desc: 'Vector iconography, logo design, custom illustration assets' },
  { name: 'Notion & Whimsical', category: 'tools', level: 'Proficient', desc: 'UX documentation, project roadmaps, sitemaps, information architecture' },

  // UX Research & Strategy
  { name: 'User Personas & Empathy Maps', category: 'ux', level: 'Advanced', desc: 'Synthesizing qualitative interview data into relatable target user profiles' },
  { name: 'User Journey Mapping', category: 'ux', level: 'Advanced', desc: 'Visualizing end-to-end user emotional journeys and friction touchpoints' },
  { name: 'Usability Testing & Task Analysis', category: 'ux', level: 'Proficient', desc: 'Running moderated user sessions, measuring time-on-task and error rates' },
  { name: 'Information Architecture (IA)', category: 'ux', level: 'Advanced', desc: 'Card sorting, clear visual hierarchies, intuitive category taxonomy' },
  { name: 'Competitive UX Benchmarking', category: 'ux', level: 'Proficient', desc: 'Analyzing rival products for market gaps and UX design patterns' },

  // UI & Visual Craft
  { name: 'Scalable Design Systems', category: 'ui', level: 'Advanced', desc: 'Atomic design tokens, typography scales, 8pt spatial rhythm' },
  { name: 'Auto-Layout & Responsive Constraints', category: 'ui', level: 'Advanced', desc: 'Fluid component responsiveness across mobile, tablet, and widescreen' },
  { name: 'Color Theory & Harmony', category: 'ui', level: 'Advanced', desc: '60-30-10 palette balance, semantic states, electric blue accents' },
  { name: 'Typography Hierarchy & Readability', category: 'ui', level: 'Advanced', desc: 'Modular scale, line-height ratios, font pairing for scanability' },
  { name: 'Micro-Interactions & State Design', category: 'ui', level: 'Proficient', desc: 'Hover, pressed, loading, error, and feedback animations' },

  // UI Prototyping & Styling
  { name: 'Tailwind CSS (UI Styling)', category: 'prototyping', level: 'Advanced', desc: 'Rapid translation of Figma mockups into clean, responsive HTML/CSS UI' },
  { name: 'Responsive Web Design', category: 'prototyping', level: 'Advanced', desc: 'Mobile-first fluid layouts, breakpoint management, touch targets' },
  { name: 'Figma Smart Animate Prototyping', category: 'prototyping', level: 'Advanced', desc: 'High-fidelity screen transitions, drag gestures, modal popups' },
  { name: 'Semantic HTML5 & Accessible CSS', category: 'prototyping', level: 'Proficient', desc: 'Screen reader accessibility, ARIA tags, zero layout shift' },

  // HCI & Usability Laws
  { name: "Jakob Nielsen's 10 Heuristics", category: 'hci', level: 'Core Knowledge', desc: 'System status visibility, error prevention, consistency, recognition over recall' },
  { name: 'WCAG 2.1 AA Accessibility', category: 'hci', level: 'Core Knowledge', desc: 'Color contrast standards (4.5:1 minimum ratio), focus indicators' },
  { name: "Fitts's Law & Hick's Law", category: 'hci', level: 'Core Knowledge', desc: 'Optimizing touch targets and reducing cognitive choice overload' }
]

const filteredSkills = computed(() => {
  if (selectedCategory.value === 'all') return skillItems
  return skillItems.filter(s => s.category === selectedCategory.value)
})
</script>

<template>
  <section id="skills" class="px-6 py-24 relative bg-[#0c1324]">
    <div class="mx-auto max-w-7xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-14">
        <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
          Design Expertise
        </p>
        <h2 class="mt-3 text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          UI/UX Skills & Capabilities
        </h2>
        <p class="mt-4 text-base text-gray-400">
          User-centered design methodologies, prototyping software, and visual interaction systems.
        </p>
      </div>

      <!-- Category Filter Tabs -->
      <div class="flex flex-wrap items-center justify-center gap-2 mb-12">
        <button
          v-for="cat in categories"
          :key="cat.id"
          @click="selectedCategory = cat.id"
          class="flex items-center gap-2 rounded-xl px-4 py-2.5 text-xs sm:text-sm font-semibold transition cursor-pointer"
          :class="[
            selectedCategory === cat.id
              ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/30'
              : 'glass-card text-gray-300 hover:text-white hover:border-blue-400'
          ]"
        >
          <component :is="cat.icon" :size="15" />
          <span>{{ cat.label }}</span>
        </button>
      </div>

      <!-- Skills Grid -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
        <div
          v-for="skill in filteredSkills"
          :key="skill.name"
          class="glass-card glass-card-hover rounded-2xl p-5 flex flex-col justify-between group border"
        >
          <div class="text-left">
            <div class="flex items-center justify-between gap-2 mb-2">
              <h3 class="font-bold text-white text-sm sm:text-base group-hover:text-blue-300 transition">
                {{ skill.name }}
              </h3>
              <span 
                class="rounded-full px-2.5 py-0.5 text-[10px] font-mono font-semibold shrink-0"
                :class="{
                  'bg-blue-500/10 text-blue-300 border border-blue-500/30': skill.level === 'Advanced',
                  'bg-cyan-500/10 text-cyan-300 border border-cyan-500/30': skill.level === 'Proficient',
                  'bg-emerald-500/10 text-emerald-300 border border-emerald-500/30': skill.level === 'Core Knowledge',
                  'bg-amber-500/10 text-amber-300 border border-amber-500/30': skill.level === 'Intermediate'
                }"
              >
                {{ skill.level }}
              </span>
            </div>
            
            <p class="text-xs text-gray-400 leading-relaxed">
              {{ skill.desc }}
            </p>
          </div>

          <!-- Bottom Visual Bar -->
          <div class="mt-4 pt-3 border-t border-white/5 flex items-center justify-between text-[11px] text-gray-500 font-mono">
            <span class="capitalize">{{ skill.category }}</span>
            <span class="text-blue-400 opacity-0 group-hover:opacity-100 transition">✦ Verified</span>
          </div>
        </div>
      </div>

      <!-- Presentation Highlight Box -->
      <div class="mt-14 rounded-3xl border border-blue-900/40 bg-gradient-to-r from-blue-950/40 via-[#0e172e] to-blue-950/40 p-6 sm:p-8">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-left">
          
          <div class="space-y-2">
            <h4 class="flex items-center gap-2 text-sm font-bold uppercase tracking-wider text-blue-400">
              <Figma :size="16" /> Design Systems First
            </h4>
            <p class="text-xs text-gray-300">
              Every project uses atomic design tokens with 100% auto-layout, clear component variants, and interactive states for smooth handoff.
            </p>
          </div>

          <div class="space-y-2">
            <h4 class="flex items-center gap-2 text-sm font-bold uppercase tracking-wider text-cyan-400">
              <Eye :size="16" /> Usability & Empathy
            </h4>
            <p class="text-xs text-gray-300">
              Guided by Jakob Nielsen's Heuristics and WCAG 2.1 AA accessibility guidelines, ensuring interfaces are usable by everyone.
            </p>
          </div>

          <div class="space-y-2">
            <h4 class="flex items-center gap-2 text-sm font-bold uppercase tracking-wider text-sky-400">
              <Layout :size="16" /> Front-of-the-Front Prototyping
            </h4>
            <p class="text-xs text-gray-300">
              Bridging design and code with high-fidelity Tailwind CSS prototypes without complex backend or database entanglements.
            </p>
          </div>

        </div>
      </div>

    </div>
  </section>
</template>