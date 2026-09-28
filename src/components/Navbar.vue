<script setup>
import { 
  Menu, 
  X, 
  FileText, 
  Figma, 
  Sparkles,
  Layers
} from "lucide-vue-next";
import { ref, onMounted, onUnmounted } from "vue";

const emit = defineEmits(['openResume'])

const isOpen = ref(false);
const isScrolled = ref(false);

const links = [
  { name: "Home", href: "#home" },
  { name: "About", href: "#about" },
  { name: "Process", href: "#process" },
  { name: "Skills", href: "#skills" },
  { name: "Case Studies", href: "#casestudies" },
  { name: "UX Lab", href: "#playground" },
  { name: "Education", href: "#education" },
  { name: "Contact", href: "#contact" },
];

const checkScroll = () => {
  isScrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener('scroll', checkScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', checkScroll);
});
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-40 transition-all duration-300"
    :class="[
      isScrolled 
        ? 'bg-[#0b1120]/90 backdrop-blur-md border-b border-blue-500/20 shadow-lg shadow-black/40 py-3' 
        : 'bg-transparent py-5'
    ]"
  >
    <div class="mx-auto flex max-w-7xl items-center justify-between px-6">
      
      <!-- Brand Logo -->
      <a href="#home" class="group flex items-center gap-2.5 text-xl font-extrabold text-white tracking-tight">
        <div class="flex h-9 w-9 items-center justify-center rounded-xl bg-gradient-to-br from-blue-600 to-cyan-500 text-white shadow-md shadow-blue-600/30 transition group-hover:scale-105">
          <Figma :size="19" />
        </div>
        <span class="tracking-wider font-extrabold">VINZ<span class="text-blue-400">.UX</span></span>
        <span class="hidden sm:inline-flex items-center gap-1.5 rounded-full bg-blue-500/10 px-2.5 py-0.5 text-[11px] font-semibold text-blue-400 border border-blue-500/20 ml-1.5">
          <span class="h-1.5 w-1.5 rounded-full bg-blue-500 animate-pulse"></span>
          UI/UX Student
        </span>
      </a>

      <!-- Desktop Navigation -->
      <nav class="hidden items-center gap-1 md:flex">
        <a
          v-for="link in links"
          :key="link.name"
          :href="link.href"
          class="rounded-lg px-3 py-1.5 text-xs lg:text-sm font-medium text-slate-300 transition hover:bg-blue-950/40 hover:text-blue-400"
        >
          {{ link.name }}
        </a>
      </nav>

      <!-- Action Button (Resume) -->
      <div class="hidden items-center gap-2.5 sm:flex">
        <button
          @click="emit('openResume')"
          class="flex items-center gap-2 rounded-xl border border-blue-500/30 bg-blue-600 text-white px-4 py-2 text-xs font-semibold shadow-md shadow-blue-600/20 transition hover:bg-blue-500 hover:scale-[1.02] active:scale-[0.98] cursor-pointer"
        >
          <FileText :size="15" />
          <span>UX Resume / CV</span>
        </button>
      </div>

      <!-- Mobile Hamburger -->
      <div class="flex items-center gap-2 md:hidden">
        <button 
          class="rounded-lg p-2 text-gray-300 hover:bg-white/5" 
          @click="isOpen = !isOpen"
          aria-label="Toggle navigation menu"
        >
          <X v-if="isOpen" :size="24" />
          <Menu v-else :size="24" />
        </button>
      </div>
    </div>

    <!-- Mobile Dropdown Menu -->
    <div 
      v-if="isOpen" 
      class="border-b border-blue-900/40 bg-[#0c1322]/95 px-6 py-5 backdrop-blur-xl md:hidden"
    >
      <div class="flex flex-col gap-2 text-left">
        <a
          v-for="link in links"
          :key="link.name"
          :href="link.href"
          class="rounded-lg px-3 py-2 text-sm font-medium text-gray-300 hover:bg-white/5 hover:text-blue-400"
          @click="isOpen = false"
        >
          {{ link.name }}
        </a>

        <div class="pt-3 border-t border-white/10 mt-2">
          <button
            @click="emit('openResume'); isOpen = false"
            class="flex w-full items-center justify-center gap-2 rounded-xl bg-blue-600 px-4 py-2.5 text-sm font-semibold text-white shadow-md transition hover:bg-blue-500"
          >
            <FileText :size="16" />
            <span>View UI/UX Resume</span>
          </button>
        </div>
      </div>
    </div>
  </header>
</template>
