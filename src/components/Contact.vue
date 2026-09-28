<script setup>
import { ref } from 'vue'
import { 
  Figma, 
  Linkedin, 
  Mail, 
  Copy, 
  Check, 
  Send, 
  MapPin, 
  Sparkles, 
  CheckCircle2,
  Globe,
  Palette
} from 'lucide-vue-next'
import confetti from 'canvas-confetti'

const emit = defineEmits(['showToast'])

const email = 'vinz.uxdesign@gmail.com'
const isCopied = ref(false)
const isSubmitting = ref(false)
const isSubmitted = ref(false)

const form = ref({
  name: '',
  email: '',
  role: 'Recruiter / Company',
  message: ''
})

const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText(email)
    isCopied.value = true
    emit('showToast', 'Designer email copied to clipboard!')
    setTimeout(() => {
      isCopied.value = false
    }, 3000)
  } catch (err) {
    emit('showToast', `Email: ${email}`)
  }
}

const handleSubmit = () => {
  if (!form.value.name || !form.value.email || !form.value.message) {
    emit('showToast', 'Please fill in all required fields.')
    return
  }

  isSubmitting.value = true
  setTimeout(() => {
    isSubmitting.value = false
    isSubmitted.value = true
    emit('showToast', 'Thank you! Your inquiry has been sent.')
    
    // Trigger confetti
    try {
      confetti({
        particleCount: 90,
        spread: 65,
        origin: { y: 0.7 }
      })
    } catch (e) {}

    // Reset form
    setTimeout(() => {
      form.value = { name: '', email: '', role: 'Recruiter / Company', message: '' }
      isSubmitted.value = false
    }, 4500)
  }, 1000)
}
</script>

<template>
  <section id="contact" class="px-6 py-24 relative bg-[#0c1324]">
    <div class="mx-auto max-w-7xl">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-16">
        <p class="text-xs sm:text-sm font-bold uppercase tracking-[0.25em] text-blue-400">
          Get In Touch
        </p>
        <h2 class="mt-3 text-3xl sm:text-5xl font-extrabold text-white tracking-tight">
          Let's Design Together
        </h2>
        <p class="mt-4 text-base text-gray-400">
          Have an internship opportunity, design sprint collaboration, or academic inquiry? Feel free to reach out!
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-12 gap-10">
        
        <!-- Left Column: Contact Cards & Info -->
        <div class="lg:col-span-5 space-y-6">
          
          <div class="glass-card rounded-3xl p-6 sm:p-8 space-y-6 border border-blue-900/40 text-left">
            <h3 class="text-xl font-bold text-white">
              Contact & Social Channels
            </h3>

            <p class="text-xs sm:text-sm text-gray-300 leading-relaxed">
              I am actively seeking <strong>UI/UX Design On-the-Job Training (OJT) / Internships</strong> for the upcoming academic cycle.
            </p>

            <div class="space-y-4">
              <!-- Email Card -->
              <div class="rounded-2xl border border-white/10 bg-white/[0.02] p-4 flex items-center justify-between gap-3 shadow-sm">
                <div class="flex items-center gap-3 overflow-hidden">
                  <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-xl bg-blue-500/20 text-blue-400">
                    <Mail :size="18" />
                  </div>
                  <div class="truncate text-left">
                    <p class="text-[11px] text-gray-400 font-medium">Direct Email</p>
                    <p class="text-xs sm:text-sm font-bold text-white truncate">{{ email }}</p>
                  </div>
                </div>

                <button
                  @click="copyEmail"
                  class="rounded-xl bg-blue-950/60 hover:bg-blue-600 p-2 text-blue-300 hover:text-white transition cursor-pointer shrink-0 border border-blue-800"
                  :title="isCopied ? 'Copied!' : 'Copy Email'"
                >
                  <Check v-if="isCopied" :size="16" class="text-emerald-400" />
                  <Copy v-else :size="16" />
                </button>
              </div>

              <!-- Location Card -->
              <div class="rounded-2xl border border-white/10 bg-white/[0.02] p-4 flex items-center gap-3 shadow-sm">
                <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-xl bg-cyan-500/20 text-cyan-400">
                  <MapPin :size="18" />
                </div>
                <div class="text-left">
                  <p class="text-[11px] text-gray-400 font-medium">Location & Work Mode</p>
                  <p class="text-xs sm:text-sm font-bold text-white">Philippines (Open for Remote / On-Site OJT)</p>
                </div>
              </div>

              <!-- Availability Status -->
              <div class="rounded-2xl border border-emerald-500/20 bg-emerald-500/5 p-4 flex items-center gap-3">
                <div class="flex h-10 w-10 shrink-0 items-center justify-center rounded-xl bg-emerald-500/20 text-emerald-400">
                  <Sparkles :size="18" />
                </div>
                <div class="text-left">
                  <p class="text-[11px] text-emerald-400 font-semibold">Availability</p>
                  <p class="text-xs sm:text-sm font-bold text-emerald-300">Ready for OJT & Capstone Design Lead</p>
                </div>
              </div>
            </div>

            <!-- Social Profiles -->
            <div class="pt-2 border-t border-white/10">
              <p class="text-xs font-mono uppercase tracking-wider text-gray-400 mb-3 text-left">Design & Professional Portfolios</p>
              <div class="flex flex-wrap gap-2.5">
                <a
                  href="https://figma.com"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-3.5 py-2 text-xs font-semibold text-gray-300 transition hover:bg-blue-600 hover:text-white hover:border-blue-600 shadow-sm"
                >
                  <Figma :size="15" />
                  <span>Figma Community</span>
                </a>

                <a
                  href="https://linkedin.com"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-3.5 py-2 text-xs font-semibold text-gray-300 transition hover:bg-blue-600 hover:text-white hover:border-blue-600 shadow-sm"
                >
                  <Linkedin :size="15" />
                  <span>LinkedIn</span>
                </a>
              </div>
            </div>

          </div>

        </div>

        <!-- Right Column: Interactive Message Form -->
        <div class="lg:col-span-7">
          <div class="glass-card rounded-3xl p-6 sm:p-8 relative border border-blue-900/40 shadow-md text-left">
            <h3 class="text-xl font-bold text-white mb-2 text-left">
              Send a Design Message
            </h3>
            <p class="text-xs sm:text-sm text-gray-400 mb-6 text-left">
              Feel free to leave feedback on my portfolio or reach out for OJT opportunities!
            </p>

            <form @submit.prevent="handleSubmit" class="space-y-4 text-left">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div>
                  <label class="block text-xs font-semibold text-gray-300 mb-1.5">Your Name *</label>
                  <input
                    v-model="form.name"
                    type="text"
                    required
                    placeholder="e.g. Professor / Design Lead"
                    class="w-full rounded-xl border border-white/10 bg-white/[0.04] px-4 py-3 text-sm text-white placeholder-gray-500 focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 focus:outline-none transition"
                  />
                </div>

                <div>
                  <label class="block text-xs font-semibold text-gray-300 mb-1.5">Your Email *</label>
                  <input
                    v-model="form.email"
                    type="email"
                    required
                    placeholder="your.email@domain.com"
                    class="w-full rounded-xl border border-white/10 bg-white/[0.04] px-4 py-3 text-sm text-white placeholder-gray-500 focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 focus:outline-none transition"
                  />
                </div>
              </div>

              <div>
                <label class="block text-xs font-semibold text-gray-300 mb-1.5">Subject / Opportunity Type</label>
                <input
                  v-model="form.role"
                  type="text"
                  placeholder="e.g. UI/UX Internship / Capstone Feedback"
                  class="w-full rounded-xl border border-white/10 bg-white/[0.04] px-4 py-3 text-sm text-white placeholder-gray-500 focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 focus:outline-none transition"
                />
              </div>

              <div>
                <label class="block text-xs font-semibold text-gray-300 mb-1.5">Message *</label>
                <textarea
                  v-model="form.message"
                  required
                  rows="4"
                  placeholder="Leave your message or design critique here..."
                  class="w-full rounded-xl border border-white/10 bg-white/[0.04] px-4 py-3 text-sm text-white placeholder-gray-500 focus:border-blue-500 focus:ring-2 focus:ring-blue-500/20 focus:outline-none transition resize-none"
                ></textarea>
              </div>

              <div class="pt-2">
                <button
                  type="submit"
                  :disabled="isSubmitting || isSubmitted"
                  class="w-full sm:w-auto inline-flex items-center justify-center gap-2 rounded-xl bg-blue-600 hover:bg-blue-500 px-7 py-3.5 text-sm font-bold text-white shadow-lg shadow-blue-600/30 transition hover:scale-[1.02] active:scale-[0.98] disabled:opacity-70 cursor-pointer"
                >
                  <CheckCircle2 v-if="isSubmitted" :size="18" class="text-white" />
                  <Send v-else-if="!isSubmitting" :size="18" />
                  <span>
                    {{ isSubmitted ? 'Message Sent Successfully!' : isSubmitting ? 'Sending Message...' : 'Send Message' }}
                  </span>
                </button>
              </div>
            </form>

          </div>
        </div>

      </div>

    </div>
  </section>
</template>