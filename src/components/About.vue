<script setup>
import { ref } from 'vue'
import { 
  Palette, 
  Search, 
  Layers, 
  Target, 
  CheckCircle2, 
  Sparkles,
  BookOpen,
  Layout,
  Figma,
  Eye,
  Smile
} from 'lucide-vue-next'

const activeTab = ref('story')

const tabs = [
  { id: 'story', label: 'My UX Journey', icon: BookOpen },
  { id: 'research', label: 'UX Research & Heuristics', icon: Search },
  { id: 'craft', label: 'Figma & Design Systems', icon: Figma },
  { id: 'goals', label: 'OJT & Capstone Goals', icon: Target },
]
</script>

<template>
  <section id="about" class="px-6 py-24 relative bg-[#0b1120]">
    <div class="mx-auto max-w-7xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
          Design Background
        </p>
        <h2 class="mt-3 text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          About Me & My Design Philosophy
        </h2>
        <p class="mt-4 text-base text-gray-400">
          A BSIT 3rd-year student who found passion at the intersection of technology, psychology, and visual design.
        </p>
      </div>

      <!-- Main Two-Column Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-10 items-start">
        
        <!-- Left Column: Interactive Tab Content -->
        <div class="lg:col-span-7 space-y-6">
          
          <!-- Tab Navigation Buttons -->
          <div class="flex flex-wrap gap-2 p-1.5 rounded-2xl bg-white/[0.03] border border-blue-900/40 shadow-sm backdrop-blur-md">
            <button
              v-for="tab in tabs"
              :key="tab.id"
              @click="activeTab = tab.id"
              class="flex items-center gap-2 rounded-xl px-4 py-2.5 text-xs sm:text-sm font-semibold transition cursor-pointer"
              :class="[
                activeTab === tab.id
                  ? 'bg-blue-600 text-white shadow-md shadow-blue-600/30'
                  : 'text-gray-400 hover:text-white hover:bg-white/5'
              ]"
            >
              <component :is="tab.icon" :size="16" />
              <span>{{ tab.label }}</span>
            </button>
          </div>

          <!-- Tab Content Display -->
          <div class="glass-card rounded-3xl p-6 sm:p-8 space-y-4 text-left">
            
            <!-- Story Tab -->
            <div v-if="activeTab === 'story'" class="space-y-4 text-gray-300 leading-relaxed text-sm sm:text-base">
              <h3 class="text-xl font-bold text-white flex items-center gap-2">
                <span>The BSIT Student Who Loves Human-Centered Design</span>
              </h3>
              <p>
                As a <strong>3rd-year Bachelor of Science in Information Technology (BSIT)</strong> student, I quickly realized that great technology is meaningless if users find it confusing or frustrating to navigate.
              </p>
              <p>
                Instead of focusing on heavy backend logic and database queries, I dedicated myself entirely to <strong>User Experience (UX) Research, User Interface (UI) Design, and Usability Engineering</strong>.
              </p>
              <p>
                My mission is to eliminate user friction by creating clean layouts, legible typography hierarchies, harmonious color palettes, and accessible interfaces that delight users on both mobile and desktop.
              </p>
            </div>

            <!-- UX Research Tab -->
            <div v-if="activeTab === 'research'" class="space-y-4 text-gray-300 leading-relaxed text-sm sm:text-base">
              <h3 class="text-xl font-bold text-white flex items-center gap-2">
                <span>Research-Driven & Usability Heuristics</span>
              </h3>
              <p>
                Every screen I design starts with understanding the user's mental model and pain points before drawing a single pixel in Figma.
              </p>
              <div class="space-y-2.5 pt-1">
                <div class="flex items-start gap-3 rounded-xl bg-blue-950/40 border border-blue-900/40 p-3">
                  <Eye :size="17" class="text-blue-400 mt-0.5 shrink-0" />
                  <div class="text-xs sm:text-sm">
                    <p class="font-bold text-blue-200">Jakob Nielsen's 10 Usability Heuristics</p>
                    <p class="text-gray-400">Ensuring visibility of system status, user control, error prevention, and consistency across all flows.</p>
                  </div>
                </div>
                <div class="flex items-start gap-3 rounded-xl bg-cyan-950/30 border border-cyan-900/40 p-3">
                  <Smile :size="17" class="text-cyan-400 mt-0.5 shrink-0" />
                  <div class="text-xs sm:text-sm">
                    <p class="font-bold text-cyan-200">Empathy Mapping & User Personas</p>
                    <p class="text-gray-400">Conducting user interviews to distill real motivations, frustrations, and behavioral patterns.</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Figma & Craft Tab -->
            <div v-if="activeTab === 'craft'" class="space-y-4 text-gray-300 leading-relaxed text-sm sm:text-base">
              <h3 class="text-xl font-bold text-white flex items-center gap-2">
                <span>Figma Mastery & Scalable Design Systems</span>
              </h3>
              <p>
                I build structured Figma files that make developer handoff seamless and scalable:
              </p>
              <ul class="space-y-2 text-xs sm:text-sm text-gray-300">
                <li class="flex items-center gap-2">
                  <CheckCircle2 :size="16" class="text-blue-400" />
                  <span><strong>100% Auto-Layout & Constraints:</strong> Fluid responsiveness for any device viewport.</span>
                </li>
                <li class="flex items-center gap-2">
                  <CheckCircle2 :size="16" class="text-blue-400" />
                  <span><strong>Interactive Component Variants:</strong> Hover, active, focus, and error state micro-interactions.</span>
                </li>
                <li class="flex items-center gap-2">
                  <CheckCircle2 :size="16" class="text-blue-400" />
                  <span><strong>Atomic Design Tokens:</strong> Reusable color swatches, typography styles, elevation, and 8pt spacing grids.</span>
                </li>
              </ul>
            </div>

            <!-- Goals Tab -->
            <div v-if="activeTab === 'goals'" class="space-y-4 text-gray-300 leading-relaxed text-sm sm:text-base">
              <h3 class="text-xl font-bold text-white flex items-center gap-2">
                <span>Internship / OJT Readiness & Capstone Lead</span>
              </h3>
              <p>
                As a 3rd-year student preparing for graduation:
              </p>
              <div class="space-y-2 pt-1">
                <div class="rounded-xl bg-blue-950/30 border border-blue-900/40 p-3">
                  <p class="font-bold text-blue-300 text-xs sm:text-sm">🎯 Target OJT / Internship Role</p>
                  <p class="text-xs text-gray-400 mt-1">Junior UI/UX Designer, Product Design Intern, or UX Researcher in tech companies.</p>
                </div>
                <div class="rounded-xl bg-cyan-950/30 border border-cyan-900/40 p-3">
                  <p class="font-bold text-cyan-300 text-xs sm:text-sm">🎓 Capstone Project Role</p>
                  <p class="text-xs text-gray-400 mt-1">Lead UI/UX Architect responsible for user journeys, usability testing, and high-fidelity prototype fidelity.</p>
                </div>
              </div>
            </div>

          </div>

        </div>

        <!-- Right Column: Student Profile Snapshot -->
        <div class="lg:col-span-5 space-y-5">
          
          <div class="glass-card rounded-3xl p-6 space-y-4 text-left">
            <h3 class="text-xs font-bold uppercase tracking-wider text-blue-400">
              Student Designer Profile
            </h3>
            
            <div class="space-y-3 text-xs sm:text-sm">
              <div class="flex justify-between border-b border-white/5 pb-2">
                <span class="text-gray-400">Degree:</span>
                <span class="font-semibold text-white">BS Information Technology</span>
              </div>
              <div class="flex justify-between border-b border-white/5 pb-2">
                <span class="text-gray-400">Year Level:</span>
                <span class="font-semibold text-blue-300">3rd Year (Junior)</span>
              </div>
              <div class="flex justify-between border-b border-white/5 pb-2">
                <span class="text-gray-400">Specialization:</span>
                <span class="font-semibold text-cyan-400">UI/UX & Product Design</span>
              </div>
              <div class="flex justify-between border-b border-white/5 pb-2">
                <span class="text-gray-400">Core Software:</span>
                <span class="font-semibold text-white">Figma, FigJam, Miro</span>
              </div>
              <div class="flex justify-between border-b border-white/5 pb-2">
                <span class="text-gray-400">UI Prototyping:</span>
                <span class="font-semibold text-white">Tailwind CSS & HTML/CSS</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-400">OJT / Internship Status:</span>
                <span class="font-semibold text-emerald-400">🟢 Available / Seeking</span>
              </div>
            </div>
          </div>

          <!-- Highlight Box -->
          <div class="rounded-3xl border border-blue-500/30 bg-gradient-to-br from-blue-950/50 via-[#111c38] to-blue-900/30 p-6 space-y-3 shadow-sm text-left">
            <div class="flex items-center gap-2 text-blue-300 font-bold text-sm">
              <Sparkles :size="18" />
              <span>Designer's Core Values</span>
            </div>
            <p class="text-xs text-gray-300 leading-relaxed">
              "Empathy for the user, precision in typography, and seamless collaboration with developers through clean design tokens."
            </p>
          </div>

        </div>

      </div>

    </div>
  </section>
</template>