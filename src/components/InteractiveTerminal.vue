<script setup>
import { ref, onMounted, nextTick } from 'vue'
import { Terminal, Sparkles, CornerDownLeft, Trash2 } from 'lucide-vue-next'

const commandInput = ref('')
const terminalLogs = ref([
  { type: 'system', text: '⚡ Welcome to Vinz Terminal v3.0 [BSIT 3rd-Year Edition]' },
  { type: 'system', text: 'Type "help" to see available commands or click any command chip below.' },
])

const availableCommands = [
  'help',
  'whoami',
  'skills',
  'projects',
  'education',
  'contact',
  'gpa',
  'capstone',
  'clear'
]

const terminalContainer = ref(null)

const scrollToBottom = async () => {
  await nextTick()
  if (terminalContainer.value) {
    terminalContainer.value.scrollTop = terminalContainer.value.scrollHeight
  }
}

const executeCommand = (cmdText) => {
  const input = (cmdText || commandInput.value).trim().toLowerCase()
  if (!input) return

  terminalLogs.value.push({ type: 'input', text: `vinz@bsit-dev:~$ ${input}` })

  switch (input) {
    case 'help':
      terminalLogs.value.push({
        type: 'output',
        text: `AVAILABLE COMMANDS:
  • whoami     : Bio, major, and current college status
  • skills     : Tech stack and programming languages
  • projects   : Academic & personal web projects
  • education  : Degree, coursework & honors
  • capstone   : Capstone project ideas & research focus
  • gpa        : Academic standing & awards
  • contact    : Email, social profiles & availability
  • matrix     : Enter the matrix mode
  • sudo hire  : Secret message for professors / recruiters
  • clear      : Clear terminal screen`
      })
      break

    case 'whoami':
      terminalLogs.value.push({
        type: 'output',
        text: `NAME    : Vinz
ROLE    : 3rd-Year BSIT College Student & Aspiring Full-Stack Developer
LOCATION: Philippines
STATUS  : 🟢 Ready for OJT (Internship) & Capstone Collaboration
PASSION : Solving real-world problems with elegant code and accessible UI`
      })
      break

    case 'skills':
      terminalLogs.value.push({
        type: 'output',
        text: `CORE SKILLS & TECH STACK:
  [Frontend]  : Vue.js 3, JavaScript (ES6+), HTML5, CSS3, Tailwind CSS, Bootstrap
  [Backend]   : PHP, Node.js, Express, RESTful APIs
  [Database]  : MySQL, PostgreSQL, Relational DB Design, Normalization
  [Tools/Env] : Git, GitHub, VS Code, Postman, Vite, Linux/Bash, Figma
  [BSIT Core] : OOP, Systems Analysis & Design (SAD), HCI, Data Structures`
      })
      break

    case 'projects':
      terminalLogs.value.push({
        type: 'output',
        text: `FEATURED ACADEMIC & WEB PROJECTS:
  1. EduTrack Pro        - Student Information & Grade Management System (PHP/MySQL)
  2. MediQueue           - Real-time Clinic Queue & Patient Booking App (Vue 3/Tailwind)
  3. CampusEvent Hub     - University QR Code Attendance & Ticket Portal (JS/SQL)
  4. DevVault            - Developer Snippets & Code Vault (Vue 3/IndexedDB)
  5. ByteMart POS        - Point-of-Sale & Inventory Analytics System (PHP/MySQL)
  
  Tip: Scroll to the Projects section to explore interactive previews!`
      })
      break

    case 'education':
      terminalLogs.value.push({
        type: 'output',
        text: `ACADEMIC PROFILE:
  • Degree     : Bachelor of Science in Information Technology (BSIT)
  • Year Level : 3rd Year (Junior Standing)
  • Timeline   : 2023 - 2027 (Expected Graduation)
  • Focus Area : Web Systems, Database Architecture & Software Engineering`
      })
      break

    case 'capstone':
      terminalLogs.value.push({
        type: 'output',
        text: `CAPSTONE INITIATIVE (3RD YEAR PREPARATION):
  • Topic Domain : Intelligent Campus Services & Healthcare Queuing Web Systems
  • Architecture : Modular REST API + Reactive Frontend + Normalized Relational DB
  • Goal         : Deploy a production-ready solution to benefit our university community!`
      })
      break

    case 'gpa':
      terminalLogs.value.push({
        type: 'output',
        text: `🏆 ACADEMIC RECOGNITION:
  • Consistent Dean's Lister Candidate
  • High Distinction in Web Development & Database Design courses
  • Active participant in college IT seminars and tech workshops`
      })
      break

    case 'contact':
      terminalLogs.value.push({
        type: 'output',
        text: `GET IN TOUCH:
  • Email   : vinz.dev.it@gmail.com
  • GitHub  : https://github.com/vinz-dev
  • Status  : Open to project collaborations, internships & inquiries!`
      })
      break

    case 'sudo hire':
    case 'hire':
      terminalLogs.value.push({
        type: 'output',
        text: `🎉 ACCESS GRANTED! You unlocked the secret command.
Thank you for considering me! I am eager to contribute, learn quickly, and build great software for your team.`
      })
      break

    case 'matrix':
      terminalLogs.value.push({
        type: 'output',
        text: `01010110 01001001 01001110 01011010 00100000 01000100 01000101 01010110
[SYSTEM]: Wake up, Neo... The matrix of code awaits. Keep learning!`
      })
      break

    case 'clear':
      terminalLogs.value = []
      break

    default:
      terminalLogs.value.push({
        type: 'error',
        text: `zsh: command not found: "${input}". Type "help" for valid commands.`
      })
      break
  }

  commandInput.value = ''
  scrollToBottom()
}

const clearTerminal = () => {
  terminalLogs.value = []
}
</script>

<template>
  <section id="terminal" class="px-6 py-20 relative bg-[#0d091a]">
    <div class="mx-auto max-w-5xl">
      
      <!-- Section Heading -->
      <div class="flex flex-col items-center text-center mb-8">
        <div class="inline-flex items-center gap-2 rounded-full border border-violet-500/30 bg-violet-500/10 px-3.5 py-1 text-xs font-medium text-violet-400">
          <Terminal :size="14" />
          <span>Interactive Presentation Widget</span>
        </div>
        <h2 class="mt-3 text-3xl sm:text-4xl font-extrabold text-white">
          Developer CLI Terminal
        </h2>
        <p class="mt-2 text-sm text-gray-400 max-w-lg">
          Try typing commands below or click any chip to test this interactive presentation feature.
        </p>
      </div>

      <!-- Terminal Window Box -->
      <div class="rounded-2xl border border-violet-500/30 bg-[#090614]/95 shadow-2xl shadow-violet-950/60 overflow-hidden font-mono">
        
        <!-- Terminal Top Bar -->
        <div class="flex items-center justify-between border-b border-white/10 bg-[#140e24] px-4 py-3">
          <div class="flex items-center gap-2">
            <span class="h-3 w-3 rounded-full bg-rose-500/80 inline-block"></span>
            <span class="h-3 w-3 rounded-full bg-amber-500/80 inline-block"></span>
            <span class="h-3 w-3 rounded-full bg-emerald-500/80 inline-block"></span>
            <span class="ml-2 text-xs text-gray-400 font-sans hidden sm:inline">vinz@bsit-workstation: ~ (zsh)</span>
          </div>

          <div class="flex items-center gap-2">
            <button 
              @click="clearTerminal"
              class="flex items-center gap-1 text-[11px] text-gray-400 hover:text-white transition px-2 py-0.5 rounded hover:bg-white/5"
              title="Clear terminal"
            >
              <Trash2 :size="12" />
              <span>Clear</span>
            </button>
          </div>
        </div>

        <!-- Terminal Output Area -->
        <div 
          ref="terminalContainer" 
          class="h-72 sm:h-80 overflow-y-auto p-4 sm:p-6 text-xs sm:text-sm space-y-2.5 leading-relaxed selection:bg-violet-600/40"
        >
          <div v-if="terminalLogs.length === 0" class="text-gray-500 italic">
            Terminal cleared. Type "help" to start again.
          </div>

          <div 
            v-for="(log, idx) in terminalLogs" 
            :key="idx"
            :class="{
              'text-violet-300 font-semibold': log.type === 'input',
              'text-emerald-400': log.type === 'system',
              'text-gray-300 whitespace-pre-wrap': log.type === 'output',
              'text-rose-400': log.type === 'error'
            }"
          >
            {{ log.text }}
          </div>
        </div>

        <!-- Quick Command Chips -->
        <div class="border-t border-white/5 bg-[#100a1f] px-4 py-2.5 flex items-center gap-1.5 flex-wrap">
          <span class="text-[11px] text-gray-500 mr-1 font-sans">Quick run:</span>
          <button 
            v-for="cmd in availableCommands"
            :key="cmd"
            @click="executeCommand(cmd)"
            class="rounded bg-violet-600/10 px-2 py-0.5 text-[11px] text-violet-300 border border-violet-500/20 hover:bg-violet-600 hover:text-white transition"
          >
            {{ cmd }}
          </button>
        </div>

        <!-- Command Input Form -->
        <form @submit.prevent="executeCommand()" class="flex items-center border-t border-white/10 bg-[#0c0817] px-4 py-3">
          <span class="text-violet-400 mr-2 font-bold text-sm select-none">❯</span>
          <input
            v-model="commandInput"
            type="text"
            placeholder="Type 'help', 'whoami', 'projects'..."
            class="w-full bg-transparent text-sm text-white placeholder-gray-500 focus:outline-none"
            spellcheck="false"
            autocomplete="off"
          />
          <button 
            type="submit"
            class="ml-2 rounded-lg bg-violet-600 p-1.5 text-white transition hover:bg-violet-500"
            title="Execute command"
          >
            <CornerDownLeft :size="14" />
          </button>
        </form>

      </div>

    </div>
  </section>
</template>
