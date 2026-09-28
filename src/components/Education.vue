<script setup>
import { GraduationCap, BookOpen, Calendar, CheckCircle2, Figma, Sparkles, Layers, Compass } from 'lucide-vue-next'

const coursework = [
  { 
    name: 'Human-Computer Interaction (HCI)', 
    code: 'IT-304', 
    tag: 'Usability & Heuristics',
    desc: 'Heuristic evaluation, user task flows, usability testing methods, and cognitive load reduction.' 
  },
  { 
    name: 'Web Systems & UI Prototyping', 
    code: 'IT-301', 
    tag: 'Responsive Layouts',
    desc: 'Translating Figma design specifications into accessible, responsive web interfaces.' 
  },
  { 
    name: 'Systems Analysis & Design (SAD)', 
    code: 'IT-302', 
    tag: 'User Journey & IA',
    desc: 'User journey mapping, information architecture, business workflow analysis, and SDLC models.' 
  },
  { 
    name: 'Information Architecture & Taxonomy', 
    code: 'IT-206', 
    tag: 'Sitemaps & Navigation',
    desc: 'Card sorting, menu hierarchy structuring, intuitive navigation systems, and mental models.' 
  },
  { 
    name: 'Mobile Interface Design (UI/UX)', 
    code: 'IT-307', 
    tag: 'Figma & Smart Animate',
    desc: 'Ergonomic mobile design patterns, touch targets, gesture interactions, and animated prototypes.' 
  },
  { 
    name: 'Visual Design & Typography Systems', 
    code: 'IT-208', 
    tag: 'Design Tokens',
    desc: '8pt spatial rhythm, modular typography scales, color harmony, and WCAG AA contrast compliance.' 
  },
  { 
    name: 'Accessibility & Universal Design (WCAG)', 
    code: 'IT-309', 
    tag: 'Inclusive UX',
    desc: 'Designing digital products usable by people with visual, auditory, and motor impairments.' 
  },
  { 
    name: 'Object-Oriented Thinking for UI', 
    code: 'IT-201', 
    tag: 'Atomic Design',
    desc: 'Applying reusable component inheritance, atomic design principles, and nested variant logic.' 
  }
]
</script>

<template>
  <section id="education" class="px-6 py-24 relative bg-[#090e1c]">
    <div class="mx-auto max-w-7xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
          Academic Track
        </p>
        <h2 class="mt-3 text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          Education & Academic Coursework
        </h2>
        <p class="mt-4 text-base text-gray-400">
          Academic foundations in Human-Computer Interaction, Information Architecture, and UI systems shaping my UX mindset.
        </p>
      </div>

      <div class="space-y-10">
        
        <!-- Primary Degree Card -->
        <div class="glass-card rounded-3xl p-6 sm:p-10 border border-blue-900/40 relative overflow-hidden text-left">
          <div class="absolute top-0 right-0 w-72 h-72 bg-blue-600/10 rounded-full blur-3xl pointer-events-none"></div>

          <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-white/10 pb-6 mb-6">
            <div>
              <div class="flex items-center gap-2 text-xs font-semibold text-blue-400 font-mono">
                <Calendar :size="15" />
                <span>2023 — 2027 (Expected Graduation)</span>
              </div>

              <h3 class="mt-2 text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
                Bachelor of Science in Information Technology (BSIT)
              </h3>

              <p class="mt-1 text-blue-300 font-medium text-sm">
                College of Computer Studies • Specializing in UI/UX & Interaction Design
              </p>
            </div>

            <div class="flex items-center gap-2">
              <span class="inline-flex items-center gap-1.5 rounded-full bg-blue-500/10 px-3.5 py-1.5 text-xs font-bold text-blue-300 border border-blue-500/20">
                <GraduationCap :size="15" />
                <span>3rd Year (Junior Standing)</span>
              </span>
            </div>
          </div>

          <p class="text-sm sm:text-base text-gray-300 leading-relaxed max-w-4xl">
            Currently completing 3rd-year major coursework focusing on Human-Computer Interaction (HCI), user journey analysis, heuristic evaluation, and mobile interface prototyping. Preparing to lead UI/UX architecture for our upcoming Capstone research project and entering On-the-Job Training (OJT).
          </p>

          <!-- Key Academic Pillars -->
          <div class="mt-8 pt-6 border-t border-white/10 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 text-xs text-gray-300">
            <div class="flex items-center gap-2.5 bg-white/[0.02] p-3 rounded-xl border border-white/5">
              <CheckCircle2 :size="16" class="text-blue-400 shrink-0" />
              <span>Junior Standing (3rd Year)</span>
            </div>
            <div class="flex items-center gap-2.5 bg-white/[0.02] p-3 rounded-xl border border-white/5">
              <CheckCircle2 :size="16" class="text-blue-400 shrink-0" />
              <span>Product Design Focus</span>
            </div>
            <div class="flex items-center gap-2.5 bg-white/[0.02] p-3 rounded-xl border border-white/5">
              <CheckCircle2 :size="16" class="text-blue-400 shrink-0" />
              <span>Capstone UI/UX Lead</span>
            </div>
            <div class="flex items-center gap-2.5 bg-white/[0.02] p-3 rounded-xl border border-white/5">
              <CheckCircle2 :size="16" class="text-blue-400 shrink-0" />
              <span>OJT (Internship) Ready</span>
            </div>
          </div>
        </div>

        <!-- Coursework Grid -->
        <div class="glass-card rounded-3xl p-6 sm:p-10 border border-blue-900/40 text-left">
          <div class="flex items-center justify-between mb-8">
            <h3 class="flex items-center gap-2.5 text-xl font-bold text-white">
              <BookOpen :size="20" class="text-blue-400" />
              <span>Key BSIT UI/UX & HCI Coursework</span>
            </h3>
            <span class="text-xs text-gray-500 font-mono hidden sm:inline">8 Core Subjects</span>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <div
              v-for="course in coursework"
              :key="course.name"
              class="rounded-2xl bg-white/[0.02] border border-white/10 p-5 flex flex-col justify-between hover:border-blue-400 transition group"
            >
              <div>
                <div class="flex items-center justify-between mb-2">
                  <span class="text-[11px] font-mono font-bold text-blue-400">{{ course.code }}</span>
                  <span class="text-[10px] rounded bg-white/5 px-2 py-0.5 text-gray-400 font-medium">{{ course.tag }}</span>
                </div>
                <h4 class="font-bold text-white text-sm group-hover:text-blue-300 transition">{{ course.name }}</h4>
                <p class="text-xs text-gray-400 mt-2 leading-relaxed">{{ course.desc }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Presentation Highlight Callout -->
        <div class="rounded-3xl border border-blue-900/40 bg-gradient-to-r from-blue-950/40 via-[#0e172e] to-blue-950/40 p-6 sm:p-8 text-left">
          <div class="flex items-start gap-4">
            <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-xl bg-blue-500/20 text-blue-400">
              <Sparkles :size="20" />
            </div>
            <div>
              <p class="text-xs font-bold uppercase tracking-wider text-blue-300">
                Academic & Practical Alignment
              </p>
              <p class="text-xs sm:text-sm text-gray-300 mt-1 leading-relaxed">
                By integrating theoretical HCI methodologies with modern Figma design workflows, I create products that balance user empathy, technical feasibility, and high visual standards.
              </p>
            </div>
          </div>
        </div>

      </div>

    </div>
  </section>
</template>