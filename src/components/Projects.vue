<script setup>
import { ref, computed } from 'vue'
import { ExternalLink, Figma, Eye, Sparkles, Layout, Smartphone, Monitor, BookOpen } from 'lucide-vue-next'
import CaseStudyModal from './CaseStudyModal.vue'

const activeCategory = ref('all')
const selectedProject = ref(null)

const categories = [
  { id: 'all', label: 'All Case Studies' },
  { id: 'mobile', label: 'Mobile App UX' },
  { id: 'web', label: 'Web Platforms' },
  { id: 'systems', label: 'Design Systems' },
]

const projects = [
  {
    id: 'studypulse',
    title: 'StudyPulse — Student Habit & Productivity App',
    badge: 'Mobile UX Case Study',
    category: 'mobile',
    filterCategory: ['mobile'],
    image: '/projects/studypulse.jpg',
    role: 'Lead UI/UX Researcher & Product Designer',
    timeline: '3 Weeks • Academic Capstone Candidate',
    description: 'A minimalist mobile companion designed to prevent college student burnout through distraction-free habit logging, visual progress charts, and focus timer micro-interactions.',
    problem: 'College students juggle intense course schedules, irregular study habits, and overwhelming notification clutter from existing LMS apps, leading to chronic task paralysis.',
    solution: 'Designed an intuitive, 3-tap habit completion flow with calm sapphire blue aesthetics, auto-scheduled focus sessions, and motivational visual streaks.',
    persona: 'Sarah (20, 3rd-Year IT College Student balancing 6 subjects & exam deadlines)',
    insights: [
      '78% of interviewed students abandoned apps with complex multi-step menus',
      'Need for clear, color-coded visual daily timeline at first glance',
      'Positive reinforcement through subtle haptic bounce animations on task completion'
    ],
    features: [
      '100% Auto-layout components with nested variants',
      'Custom 8pt spacing grid and legible typographic scale',
      'Dark & Light mode token compatibility',
      'Interactive Smart Animate micro-interactions'
    ],
    technologies: ['Figma', 'User Research', 'Auto-Layout', 'Interactive Variants', 'Micro-Interactions'],
    figmaLink: 'https://figma.com'
  },
  {
    id: 'lumina',
    title: 'Lumina Health — Telehealth & Appointment Portal',
    badge: 'Web App Redesign & Accessibility',
    category: 'web',
    filterCategory: ['web'],
    image: '/projects/lumina.jpg',
    role: 'UI/UX Designer & Accessibility Specialist',
    timeline: '4 Weeks • HCI Course Project',
    description: 'A responsive desktop & tablet telehealth consultation dashboard designed with high-contrast accessibility (WCAG 2.1 AA) and frictionless 2-step booking.',
    problem: 'Patients with varying digital literacy and visual impairments suffered high drop-off rates on crowded clinical portals with small fonts and confusing doctor schedules.',
    solution: 'Restructured the information architecture using modular card layouts, 16px+ legible typography, clear live queue status indicators, and keyboard navigation support.',
    persona: 'James (45, Remote Worker managing chronic health consultations for family)',
    insights: [
      'Users prioritized seeing immediate doctor availability over lengthy bio text',
      'High demand for clear visual feedback during appointment confirmation',
      'Achieved 100% WCAG 2.1 AA contrast compliance across all interactive states'
    ],
    features: [
      '2-Step seamless doctor consultation reservation flow',
      'Live queue status monitor with pulse state indicators',
      'Responsive desktop and tablet breakpoints',
      'Accessible color token system with 4.8:1 minimum contrast'
    ],
    technologies: ['Figma', 'WCAG 2.1 AA', 'Information Architecture', 'Heuristic Evaluation', 'Responsive Web UI'],
    figmaLink: 'https://figma.com'
  },
  {
    id: 'campusbite',
    title: 'CampusBite — University Cafeteria Pre-Ordering App',
    badge: 'Mobile Interaction Design',
    category: 'mobile',
    filterCategory: ['mobile'],
    image: '/projects/campusbite.jpg',
    role: 'UI/UX Student Designer',
    timeline: '2 Weeks • University UX Sprint',
    description: 'A fast-paced food ordering mobile UI designed to eliminate 45-minute cafeteria lunch queues with instant student discount badges and live order tracking.',
    problem: 'University cafeteria lines during 12:00 PM peak hours caused students to skip meals or arrive late to afternoon classes.',
    solution: 'Engineered a one-thumb navigation layout with quick food categorization, instant student discount calculation, and an animated progress bar from kitchen to pickup counter.',
    persona: 'Alex (19, College Sophomore with a tight 30-minute lunch break)',
    insights: [
      'Average order completion time decreased by 62% in prototype usability tests',
      'Bottom-sheet cart modal minimized context switching',
      'Visual food imagery increased student satisfaction rating to 94%'
    ],
    features: [
      'One-thumb ergonomic interactive navigation',
      'Real-time order countdown ticker and notification banner',
      'Dynamic student discount toggle with instant price refresh',
      'Comprehensive UI component library in Figma'
    ],
    technologies: ['Figma', 'Usability Testing', 'User Journey Mapping', 'Mobile UI', 'Figma Smart Animate'],
    figmaLink: 'https://figma.com'
  },
  {
    id: 'aurora',
    title: 'Aurora UI Kit — Scalable Figma Design System',
    badge: 'Design System & Component Library',
    category: 'systems',
    filterCategory: ['systems', 'web'],
    image: '/projects/aurora.jpg',
    role: 'Design System Architect',
    timeline: 'Ongoing • Student Toolkit',
    description: 'A comprehensive, multi-theme design system and UI library featuring 120+ atomic components, semantic color tokens in electric blue, and responsive guidelines.',
    problem: 'Inconsistent typography, mismatched button padding, and fragmented styles caused immense friction and visual incoherence across collegiate group projects.',
    solution: 'Created an open design system with strict naming conventions, accessible semantic tokens, and production-ready component sets ready for developer handoff.',
    persona: 'Designers & Frontend Students needing cohesive UI building blocks',
    insights: [
      'Reduced design iteration time by over 50% for class teammates',
      'Seamless light and dark mode switching with organized Figma color styles',
      'Comprehensive documentation covering button hierarchy, input states, and dialogs'
    ],
    features: [
      '120+ Auto-layout component sets with component properties',
      'Complete typography scale based on a 1.250 Major Third ratio',
      'Comprehensive states: Default, Hover, Focused, Active, Disabled, Error',
      'Light & Dark mode design token variables'
    ],
    technologies: ['Figma Component Props', 'Design Tokens', 'Atomic Design', 'Typography Scales', 'Theme Tokens'],
    figmaLink: 'https://figma.com'
  }
]

const filteredProjects = computed(() => {
  if (activeCategory.value === 'all') return projects
  return projects.filter(p => p.filterCategory.includes(activeCategory.value))
})

const openDetailModal = (project) => {
  selectedProject.value = project
}

const closeDetailModal = () => {
  selectedProject.value = null
}
</script>

<template>
  <section id="casestudies" class="px-6 py-24 relative bg-[#090e1c]">
    <div class="mx-auto max-w-7xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-14">
        <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
          Selected Portfolio Work
        </p>
        <h2 class="mt-3 text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          Featured UI/UX Case Studies
        </h2>
        <p class="mt-4 text-base text-gray-400">
          User research, information architecture, interactive prototypes, and design systems.
        </p>
      </div>

      <!-- Category Filter Tabs -->
      <div class="flex flex-wrap items-center justify-center gap-2 mb-12">
        <button
          v-for="cat in categories"
          :key="cat.id"
          @click="activeCategory = cat.id"
          class="rounded-xl px-4 py-2 text-xs sm:text-sm font-semibold transition cursor-pointer"
          :class="[
            activeCategory === cat.id
              ? 'bg-blue-600 text-white shadow-lg shadow-blue-600/30'
              : 'glass-card text-gray-300 hover:text-white hover:border-blue-400'
          ]"
        >
          {{ cat.label }}
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="grid gap-8 md:grid-cols-2 lg:grid-cols-2">
        <article
          v-for="project in filteredProjects"
          :key="project.id"
          class="group glass-card glass-card-hover rounded-3xl overflow-hidden flex flex-col justify-between border border-blue-900/40 transition-all duration-300"
        >
          <!-- Project Image & Overlay -->
          <div class="relative overflow-hidden aspect-video bg-[#0d1527]">
            <img
              :src="project.image"
              :alt="project.title"
              class="h-full w-full object-cover object-top transition duration-700 group-hover:scale-105"
            />
            
            <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-transparent opacity-70"></div>
            
            <!-- Category Badge -->
            <div class="absolute top-4 left-4">
              <span class="rounded-full bg-blue-950/80 backdrop-blur-md px-3 py-1 text-xs font-semibold text-blue-300 border border-blue-500/30 shadow-md">
                {{ project.badge }}
              </span>
            </div>

            <!-- Quick View Case Study Overlay Button -->
            <button 
              @click="openDetailModal(project)"
              class="absolute bottom-4 right-4 flex items-center gap-1.5 rounded-xl bg-blue-600 hover:bg-blue-500 px-3.5 py-1.5 text-xs font-bold text-white shadow-lg backdrop-blur-md transition cursor-pointer"
            >
              <Eye :size="14" />
              <span>Read Case Study</span>
            </button>
          </div>

          <!-- Case Study Content Body -->
          <div class="p-6 sm:p-7 flex-1 flex flex-col justify-between space-y-5 text-left">
            <div>
              <h3 class="text-xl sm:text-2xl font-bold text-white group-hover:text-blue-300 transition">
                {{ project.title }}
              </h3>

              <p class="mt-3 text-xs sm:text-sm text-gray-300 leading-relaxed">
                {{ project.description }}
              </p>
            </div>

            <div class="space-y-4 pt-2">
              <!-- Design Tags -->
              <div class="flex flex-wrap gap-1.5">
                <span
                  v-for="tech in project.technologies"
                  :key="tech"
                  class="rounded-lg bg-white/5 border border-white/10 px-2.5 py-1 text-[11px] font-mono font-medium text-blue-300"
                >
                  {{ tech }}
                </span>
              </div>

              <!-- Action Links Footer -->
              <div class="flex items-center justify-between border-t border-white/10 pt-4 text-xs font-semibold">
                <button
                  @click="openDetailModal(project)"
                  class="text-blue-400 hover:text-blue-300 flex items-center gap-1 transition cursor-pointer"
                >
                  <Eye :size="14" />
                  <span>Case Study Walkthrough</span>
                </button>

                <div class="flex items-center gap-3">
                  <a
                    :href="project.figmaLink"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="flex items-center gap-1 text-gray-400 hover:text-blue-400 transition"
                  >
                    <Figma :size="14" />
                    <span>Figma</span>
                  </a>
                </div>
              </div>

            </div>
          </div>
        </article>
      </div>

    </div>

    <!-- Case Study Modal -->
    <CaseStudyModal 
      :project="selectedProject" 
      @close="closeDetailModal" 
    />
  </section>
</template>