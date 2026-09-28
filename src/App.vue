<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import DesignProcess from './components/DesignProcess.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import DesignPlayground from './components/DesignPlayground.vue'
import Education from './components/Education.vue'
import Contact from './components/Contact.vue'
import ResumeModal from './components/ResumeModal.vue'
import Toast from './components/Toast.vue'
import { ArrowUp, Figma, Sparkles } from 'lucide-vue-next'

// Modals and Toasts
const isResumeOpen = ref(false)
const showBackToTop = ref(false)

const toastVisible = ref(false)
const toastMessage = ref('')
let toastTimeout = null

const triggerToast = (msg) => {
  toastMessage.value = msg
  toastVisible.value = true
  if (toastTimeout) clearTimeout(toastTimeout)
  toastTimeout = setTimeout(() => {
    toastVisible.value = false
  }, 3500)
}

const checkScroll = () => {
  showBackToTop.value = window.scrollY > 400
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => {
  window.addEventListener('scroll', checkScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', checkScroll)
  if (toastTimeout) clearTimeout(toastTimeout)
})
</script>

<template>
  <div class="min-h-screen bg-[#0b1120] text-slate-200 selection:bg-blue-500/30 selection:text-blue-200">
    
    <!-- Top Sticky Navigation -->
    <Navbar 
      @openResume="isResumeOpen = true" 
    />

    <!-- Main Content Sections -->
    <main>
      <Hero 
        @openResume="isResumeOpen = true" 
      />
      
      <About />

      <!-- Double Diamond 5-Step Design Process -->
      <DesignProcess />
      
      <Skills />
      
      <Projects />

      <!-- Interactive Classroom UX Lab / Design Playground -->
      <DesignPlayground 
        @showToast="triggerToast"
      />
      
      <Education />
      
      <Contact 
        @showToast="triggerToast" 
      />
    </main>

    <!-- Footer -->
    <footer class="border-t border-blue-950 bg-[#070b16] py-12 px-6">
      <div class="mx-auto max-w-7xl flex flex-col md:flex-row items-center justify-between gap-6">
        
        <!-- Left Brand & Designer Tag -->
        <div class="flex items-center gap-3 text-center md:text-left">
          <div class="flex h-9 w-9 items-center justify-center rounded-xl bg-blue-500/20 text-blue-400">
            <Figma :size="19" />
          </div>
          <div>
            <p class="font-bold text-white tracking-wide">VINZ — BSIT 3rd Year UI/UX Designer</p>
            <p class="text-xs text-gray-400">Human-Centered Digital Experiences • OJT & Internship Ready</p>
          </div>
        </div>

        <!-- Quick Jump Links -->
        <div class="flex flex-wrap justify-center gap-5 text-xs text-gray-400 font-medium">
          <a href="#home" class="hover:text-blue-400 transition">Home</a>
          <a href="#about" class="hover:text-blue-400 transition">About</a>
          <a href="#process" class="hover:text-blue-400 transition">Process</a>
          <a href="#skills" class="hover:text-blue-400 transition">Skills</a>
          <a href="#casestudies" class="hover:text-blue-400 transition">Case Studies</a>
          <a href="#playground" class="hover:text-blue-400 transition">UX Lab</a>
          <a href="#education" class="hover:text-blue-400 transition">Education</a>
          <a href="#contact" class="hover:text-blue-400 transition">Contact</a>
        </div>

        <!-- Copyright -->
        <div class="text-xs text-gray-500 text-center md:text-right">
          <p>© 2026 Vinz Design. Crafted with Vue 3 & Tailwind CSS.</p>
        </div>

      </div>
    </footer>

    <!-- Interactive UI/UX Resume Modal -->
    <ResumeModal 
      :isOpen="isResumeOpen" 
      @close="isResumeOpen = false" 
    />

    <!-- Toast Notification -->
    <Toast 
      :visible="toastVisible" 
      :message="toastMessage" 
    />

    <!-- Floating Back to Top Button -->
    <button
      v-if="showBackToTop"
      @click="scrollToTop"
      class="fixed bottom-6 left-6 z-40 flex h-11 w-11 items-center justify-center rounded-2xl border border-blue-500/30 bg-blue-600 text-white shadow-xl backdrop-blur-md transition hover:bg-blue-500 hover:scale-110 active:scale-95 cursor-pointer"
      title="Scroll to top"
      aria-label="Back to top"
    >
      <ArrowUp :size="18" />
    </button>

  </div>
</template>