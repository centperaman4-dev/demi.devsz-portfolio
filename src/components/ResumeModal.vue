<script setup>
import { 
  X, 
  Download, 
  Printer, 
  Mail, 
  MapPin, 
  Figma, 
  Linkedin, 
  GraduationCap, 
  Layers, 
  CheckCircle2, 
  Palette
} from 'lucide-vue-next'

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['close'])

const handlePrint = () => {
  window.print()
}
</script>

<template>
  <div 
    v-if="isOpen" 
    class="fixed inset-0 z-50 flex items-center justify-center p-4 sm:p-6 md:p-10 overflow-y-auto bg-black/85 backdrop-blur-md animate-fadeIn"
    @click.self="emit('close')"
  >
    <div class="relative w-full max-w-4xl max-h-[90vh] overflow-y-auto rounded-3xl border border-blue-900/60 bg-[#0f172a] p-6 sm:p-8 text-slate-200 shadow-2xl shadow-blue-950/40">
      
      <!-- Modal Header Action Bar -->
      <div class="flex items-center justify-between border-b border-white/10 pb-4 mb-6">
        <div class="flex items-center gap-2 text-blue-400 font-mono text-xs uppercase tracking-wider font-bold">
          <Palette :size="16" />
          <span>UI/UX Designer • Academic Profile</span>
        </div>
        
        <div class="flex items-center gap-2">
          <button 
            @click="handlePrint"
            class="flex items-center gap-1.5 rounded-xl bg-blue-950/60 px-3.5 py-1.5 text-xs font-bold text-blue-300 border border-blue-800 transition hover:bg-blue-600 hover:text-white cursor-pointer"
            title="Print / Save as PDF"
          >
            <Printer :size="14" />
            <span class="hidden sm:inline">Print / Save PDF</span>
          </button>
          
          <button 
            @click="emit('close')"
            class="rounded-xl p-1.5 text-slate-400 hover:bg-white/10 hover:text-white transition"
            aria-label="Close modal"
          >
            <X :size="20" />
          </button>
        </div>
      </div>

      <!-- Printable Resume Content -->
      <div id="resume-printable" class="space-y-6 text-left">
        
        <!-- Header Info -->
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 border-b border-white/10 pb-6">
          <div>
            <h1 class="text-3xl font-black text-white tracking-tight">VINZ</h1>
            <p class="text-blue-400 font-bold text-base mt-1">
              3rd Year BSIT Student • UI/UX & Product Designer
            </p>
            <p class="text-xs text-gray-400 mt-1 max-w-md">
              Specialized in user research, wireframing, high-fidelity Figma design systems, and accessible interaction design.
            </p>
          </div>
          
          <div class="space-y-1.5 text-xs text-gray-300 sm:text-right">
            <p class="flex items-center sm:justify-end gap-1.5">
              <Mail :size="14" class="text-blue-400" /> vinz.uxdesign@gmail.com
            </p>
            <p class="flex items-center sm:justify-end gap-1.5">
              <MapPin :size="14" class="text-blue-400" /> Philippines (Open for UI/UX Internship / OJT)
            </p>
            <p class="flex items-center sm:justify-end gap-1.5">
              <Figma :size="14" class="text-blue-400" /> figma.com/@vinz_design
            </p>
          </div>
        </div>

        <!-- Two Column Content -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          
          <!-- Left Column (Education & Academic Skills) -->
          <div class="space-y-6 md:col-span-1 border-b md:border-b-0 md:border-r border-white/10 pb-6 md:pb-0 md:pr-6">
            <!-- Education -->
            <div>
              <h2 class="flex items-center gap-2 text-xs font-bold uppercase tracking-wider text-blue-400 mb-3">
                <GraduationCap :size="16" /> Education
              </h2>
              <div class="space-y-2">
                <p class="text-sm font-bold text-white">Bachelor of Science in Information Technology (BSIT)</p>
                <p class="text-xs text-gray-300">College of Computer Studies</p>
                <span class="inline-block rounded-md bg-blue-950/40 px-2 py-0.5 text-[11px] font-mono text-blue-300 border border-blue-800">
                  3rd Year • 2023 - 2027 (Expected)
                </span>
                <p class="text-xs text-blue-300 font-semibold mt-1">Specialization: UI/UX & Interaction Design</p>
              </div>
            </div>

            <!-- Key Coursework -->
            <div>
              <h2 class="text-xs font-bold uppercase tracking-wider text-blue-400 mb-2">Key Coursework</h2>
              <ul class="text-xs text-gray-400 space-y-1 list-disc list-inside">
                <li>Human-Computer Interaction (HCI)</li>
                <li>Web Systems & UI Prototyping</li>
                <li>Systems Analysis & Design (SAD)</li>
                <li>Information Architecture & Taxonomy</li>
                <li>Accessibility & Universal Design (WCAG)</li>
                <li>Visual Design & Typography Systems</li>
              </ul>
            </div>

            <!-- UI/UX Skills -->
            <div>
              <h2 class="text-xs font-bold uppercase tracking-wider text-blue-400 mb-2">Design Toolkit</h2>
              <div class="flex flex-wrap gap-1.5">
                <span v-for="skill in ['Figma', 'FigJam', 'Auto-Layout', 'Design Systems', 'User Research', 'Usability Testing', 'Heuristic Evaluation', 'Tailwind CSS', 'Miro', 'WCAG AA']" 
                  :key="skill"
                  class="rounded bg-white/5 px-2 py-0.5 text-[11px] text-gray-300 border border-white/10 font-medium">
                  {{ skill }}
                </span>
              </div>
            </div>
          </div>

          <!-- Right Column (Featured UI/UX Case Studies) -->
          <div class="space-y-6 md:col-span-2">
            <div>
              <h2 class="flex items-center gap-2 text-xs font-bold uppercase tracking-wider text-blue-400 mb-4">
                <Layers :size="16" /> Featured UI/UX Case Studies
              </h2>

              <div class="space-y-3.5">
                <div class="rounded-2xl bg-white/[0.02] border border-white/10 p-3.5">
                  <div class="flex items-center justify-between">
                    <h3 class="text-sm font-bold text-white">StudyPulse — Student Habit & Productivity App</h3>
                    <span class="text-[11px] text-blue-400 font-mono">Mobile UX</span>
                  </div>
                  <p class="text-xs text-gray-400 mt-1.5 leading-relaxed">
                    Designed a 3-tap habit completion mobile UI reducing student cognitive friction. Created 24 auto-layout screens, interactive smart animations, and dark/light mode tokens.
                  </p>
                </div>

                <div class="rounded-2xl bg-white/[0.02] border border-white/10 p-3.5">
                  <div class="flex items-center justify-between">
                    <h3 class="text-sm font-bold text-white">Lumina Health — Telehealth Consultation Portal</h3>
                    <span class="text-[11px] text-blue-400 font-mono">Web Redesign</span>
                  </div>
                  <p class="text-xs text-gray-400 mt-1.5 leading-relaxed">
                    Restructured clinical dashboard with WCAG 2.1 AA accessibility guidelines, 2-step booking flow, and responsive desktop/tablet layouts.
                  </p>
                </div>

                <div class="rounded-2xl bg-white/[0.02] border border-white/10 p-3.5">
                  <div class="flex items-center justify-between">
                    <h3 class="text-sm font-bold text-white">CampusBite — University Cafeteria Pre-Ordering App</h3>
                    <span class="text-[11px] text-blue-400 font-mono">HCI Project</span>
                  </div>
                  <p class="text-xs text-gray-400 mt-1.5 leading-relaxed">
                    Engineered an ergonomic one-thumb food ordering interface with real-time pickup countdown. Achieved 94% task completion rate in usability tests.
                  </p>
                </div>
              </div>
            </div>

            <!-- Soft Skills & Strengths -->
            <div>
              <h2 class="flex items-center gap-2 text-xs font-bold uppercase tracking-wider text-blue-400 mb-3">
                Core Strengths
              </h2>
              <div class="grid grid-cols-2 gap-2 text-xs text-gray-300">
                <div class="flex items-center gap-2">
                  <CheckCircle2 :size="14" class="text-emerald-400 shrink-0" />
                  <span>Empathy-Driven Research</span>
                </div>
                <div class="flex items-center gap-2">
                  <CheckCircle2 :size="14" class="text-emerald-400 shrink-0" />
                  <span>Figma Auto-Layout & Variants</span>
                </div>
                <div class="flex items-center gap-2">
                  <CheckCircle2 :size="14" class="text-emerald-400 shrink-0" />
                  <span>Developer Handoff Ready</span>
                </div>
                <div class="flex items-center gap-2">
                  <CheckCircle2 :size="14" class="text-emerald-400 shrink-0" />
                  <span>Clean Visual Hierarchy</span>
                </div>
              </div>
            </div>

          </div>
        </div>

        <!-- Footer Callout -->
        <div class="rounded-2xl border border-blue-900/40 bg-blue-950/30 p-4 text-center">
          <p class="text-xs text-blue-300">
            🟢 Ready for <strong>UI/UX Design Internship / OJT</strong> & Capstone Collaboration. Open to discussing Junior Product Designer roles!
          </p>
        </div>

      </div>

    </div>
  </div>
</template>

<style scoped>
@keyframes fadeIn {
  from { opacity: 0; transform: scale(0.98); }
  to { opacity: 1; transform: scale(1); }
}
.animate-fadeIn {
  animation: fadeIn 0.2s ease-out forwards;
}

@media print {
  body * {
    visibility: hidden;
  }
  #resume-printable, #resume-printable * {
    visibility: visible;
    color: black !important;
    background: white !important;
    border-color: #ddd !important;
  }
  #resume-printable {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    padding: 20px;
  }
}
</style>
