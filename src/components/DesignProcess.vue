<script setup>
import { ref } from 'vue'
import { 
  Search, 
  Compass, 
  PenTool, 
  Layout, 
  Sparkles, 
  CheckCircle2, 
  ArrowRight,
  Eye,
  Sliders,
  Users
} from 'lucide-vue-next'

const selectedStep = ref(0)

const steps = [
  {
    number: '01',
    title: 'Discover & Empathize',
    icon: Search,
    subtitle: 'Understanding real user pain points and motivations',
    summary: 'Before designing any interface, I conduct qualitative user research to uncover what real people struggle with in their daily tasks.',
    activities: [
      '1-on-1 User Interviews & Student Surveys',
      'Empathy Mapping (Says, Thinks, Does, Feels)',
      'Competitive Usability Audits',
      'Defining Primary & Secondary User Personas'
    ],
    tools: ['FigJam', 'Google Forms', 'Miro', 'Notion'],
    deliverables: 'User Personas, Empathy Maps, Key Insights Summary'
  },
  {
    number: '02',
    title: 'Define & Structure',
    icon: Compass,
    subtitle: 'Formulating the problem statement & Information Architecture',
    summary: 'Synthesizing research data into actionable "How Might We" statements and organizing intuitive navigation structures.',
    activities: [
      'Information Architecture (IA) & Sitemaps',
      'User Journey Mapping & Touchpoint Analysis',
      'Card Sorting & Navigation Hierarchy',
      'Core User Flow Diagrams'
    ],
    tools: ['FigJam', 'Whimsical', 'Figma'],
    deliverables: 'Sitemaps, User Journey Maps, Task Flows'
  },
  {
    number: '03',
    title: 'Wireframing & Lo-Fi',
    icon: PenTool,
    subtitle: 'Rapid ideation and structural layout exploration',
    summary: 'Focusing strictly on content hierarchy and interaction logic using grayscale wireframes before adding colors or imagery.',
    activities: [
      'Paper & Digital Sketching (Crazy Eights)',
      'Low-Fidelity Grayscale Wireframes',
      'Layout Composition & 8pt Grid Alignment',
      'Early Concept Feedback & Peer Critique'
    ],
    tools: ['Figma (Grayscale Kits)', 'Pencil & Paper'],
    deliverables: 'Lo-Fi Wireframe Decks, Clickable Wireflow'
  },
  {
    number: '04',
    title: 'Visual UI & Design System',
    icon: Layout,
    subtitle: 'Crafting pixel-perfect components & design tokens',
    summary: 'Bringing interfaces to life with accessible color palettes, typography scales, micro-interactions, and reusable Figma component sets.',
    activities: [
      'Atomic Design System (Buttons, Inputs, Cards)',
      'Auto-Layout & Responsive Constraints',
      'WCAG 2.1 AA Color Contrast Compliance',
      'Interactive State Variants (Hover, Focus, Active, Error)'
    ],
    tools: ['Figma', 'Stark Plugin', 'Tailwind UI'],
    deliverables: 'High-Fidelity UI Screens, Design Token Library'
  },
  {
    number: '05',
    title: 'Prototype & Usability Test',
    icon: Sparkles,
    subtitle: 'Interactive testing, validation, and iterative refinement',
    summary: 'Linking screens into realistic animated prototypes to test with real users and measure task completion times.',
    activities: [
      'Interactive Smart Animate Figma Prototypes',
      'Moderated & Unmoderated Usability Testing',
      'Heuristic Evaluation (Nielsen Norman Group)',
      'Post-Test UX Iterations & Developer Handoff'
    ],
    tools: ['Figma Prototype Mode', 'Maze', 'Loom'],
    deliverables: 'Interactive Prototype, Usability Report, Design Specs'
  }
]
</script>

<template>
  <section id="process" class="px-6 py-24 relative bg-[#090e1c]">
    <div class="mx-auto max-w-7xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
          Methodology & Craft
        </p>
        <h2 class="mt-3 text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          My UI/UX Design Process
        </h2>
        <p class="mt-4 text-base text-gray-400">
          A structured 5-stage human-centered approach to solve problems systematically and create delightful products.
        </p>
      </div>

      <!-- Step Selector Pills -->
      <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-3 mb-10">
        <button
          v-for="(step, idx) in steps"
          :key="step.number"
          @click="selectedStep = idx"
          class="rounded-2xl p-4 text-left transition cursor-pointer border flex flex-col justify-between group"
          :class="[
            selectedStep === idx
              ? 'bg-blue-600 text-white border-blue-500 shadow-lg shadow-blue-600/30'
              : 'glass-card text-slate-300 hover:border-blue-400'
          ]"
        >
          <div class="flex items-center justify-between mb-3">
            <span 
              class="font-mono text-xs font-extrabold"
              :class="selectedStep === idx ? 'text-blue-200' : 'text-blue-400'"
            >
              {{ step.number }}
            </span>
            <component 
              :is="step.icon" 
              :size="18" 
              :class="selectedStep === idx ? 'text-white' : 'text-blue-400 group-hover:scale-110 transition'"
            />
          </div>
          <p class="font-bold text-xs sm:text-sm leading-snug">
            {{ step.title }}
          </p>
        </button>
      </div>

      <!-- Active Step Deep-Dive Card -->
      <div class="glass-card rounded-3xl p-6 sm:p-10 border border-blue-900/40 relative overflow-hidden">
        <div class="absolute top-0 right-0 w-64 h-64 bg-blue-600/15 rounded-full blur-3xl pointer-events-none"></div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
          
          <!-- Left: Overview & Deliverables -->
          <div class="lg:col-span-6 space-y-5 text-left">
            <div class="inline-flex items-center gap-2 rounded-full bg-blue-950/40 px-3 py-1 text-xs font-semibold text-blue-300 border border-blue-900/40">
              <span>Phase {{ steps[selectedStep].number }}</span>
              <span>•</span>
              <span>{{ steps[selectedStep].subtitle }}</span>
            </div>

            <h3 class="text-2xl sm:text-3xl font-extrabold text-white">
              {{ steps[selectedStep].title }}
            </h3>

            <p class="text-sm sm:text-base text-gray-300 leading-relaxed">
              {{ steps[selectedStep].summary }}
            </p>

            <div class="pt-2 border-t border-white/10 space-y-2">
              <p class="text-xs font-mono uppercase tracking-wider text-blue-400 font-bold">Primary Deliverables:</p>
              <p class="text-xs sm:text-sm font-semibold text-white bg-blue-950/30 p-3 rounded-xl border border-blue-900/40">
                📦 {{ steps[selectedStep].deliverables }}
              </p>
            </div>
          </div>

          <!-- Right: Key Activities & Tools Matrix -->
          <div class="lg:col-span-6 space-y-6 text-left">
            <div>
              <h4 class="text-xs font-bold uppercase tracking-wider text-blue-400 mb-3">
                Key Activities & Techniques
              </h4>
              <ul class="space-y-2.5">
                <li
                  v-for="(act, idx) in steps[selectedStep].activities"
                  :key="idx"
                  class="flex items-start gap-2.5 text-xs sm:text-sm text-gray-300 bg-white/[0.02] p-3 rounded-xl border border-white/5"
                >
                  <CheckCircle2 :size="16" class="text-blue-400 shrink-0 mt-0.5" />
                  <span>{{ act }}</span>
                </li>
              </ul>
            </div>

            <div>
              <h4 class="text-xs font-bold uppercase tracking-wider text-blue-400 mb-2">
                Tools Employed:
              </h4>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tool in steps[selectedStep].tools"
                  :key="tool"
                  class="rounded-lg bg-blue-500/10 px-3 py-1 text-xs font-semibold text-blue-300 border border-blue-500/20 font-mono"
                >
                  {{ tool }}
                </span>
              </div>
            </div>
          </div>

        </div>

      </div>

    </div>
  </section>
</template>
