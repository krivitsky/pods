<template>
  <v-app>
    <!-- Simple Navigation Bar -->
    <v-app-bar color="white" elevation="1">
      <v-container class="pa-0" fluid>
        <div class="d-flex align-center">
          <div class="d-flex align-center" style="margin-left: 16px">
            <v-img
              :src="logo"
              alt="PODS Logo"
              width="40"
              height="40"
            />
            <span class="text-h6 text-grey-darken-1 ml-3">PODS</span>
          </div>
          <v-spacer></v-spacer>
        </div>
      </v-container>
    </v-app-bar>

    <!-- Main Content -->
    <v-main>
      <v-container class="pt-2 pb-4">
        <!-- Hero Section -->
        <v-row>
          <v-col cols="12" md="10" class="mx-auto text-center">
            <h1 class="text-h2 font-weight-bold mb-2">
              PODS
            </h1>
            <h2 class="text-h4 font-weight-medium mb-6" style="letter-spacing: 0.5px">
              PODS ORGANIZATIONAL DESIGN SYSTEM
            </h2>
          </v-col>
        </v-row>

        <!-- Main Content Area -->
        <v-row>
          <!-- Definition Block -->
          <v-col cols="12" md="6" class="pr-md-12">
            <v-card class="definition-card pa-8 mb-8" variant="outlined">
              <div class="text-h4 text-md-h4 text-sm-h5 font-weight-bold" style="line-height: 1.4;">
                "PODS" stands for Pods Organizational Design System optimizing for higher organizational intelligence in service of solving complex problems at scale with adaptive, human-centric and modular org design.
              </div>
              <div class="text-h6 text-md-h6 font-weight-regular mt-8" style="line-height: 1.4; opacity: 0.87;">
                In simpler words: With a 50-person pod, you can do pretty meaningful things!
              </div>
            </v-card>
          </v-col>

          <!-- Role Cards -->
          <v-col cols="12" md="6">
            <div 
              v-for="(role, index) in roles" 
              :key="index"
              class="role-section mb-8"
            >
              <h3 class="text-h5 mb-4">{{ role.title }}</h3>
              <p class="text-body-1 text-grey-darken-1">{{ role.description }}</p>
            </div>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <!-- Footer -->
    <v-footer class="bg-grey-lighten-4">
      <v-container class="text-center">
        © {{ new Date().getFullYear() }} PODS
      </v-container>
    </v-footer>
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import logoSvg from './assets/logo.svg'

const logo = ref(logoSvg)
const audio = ref(null)
const isPlaying = ref(false)
const audioProgress = ref(0)
const currentTime = ref(0)
const duration = ref(1565) // 26:05 in seconds

onMounted(() => {
  audio.value = new Audio('/audio/pods-intro.mp3')
  audio.value.addEventListener('timeupdate', updateProgress)
  audio.value.addEventListener('loadedmetadata', () => {
    duration.value = audio.value.duration
  })
})

const togglePlay = () => {
  if (isPlaying.value) {
    audio.value.pause()
  } else {
    audio.value.play()
  }
  isPlaying.value = !isPlaying.value
}

const updateProgress = () => {
  if (audio.value) {
    currentTime.value = audio.value.currentTime
    audioProgress.value = (audio.value.currentTime / audio.value.duration) * 100
  }
}

const seekAudio = (value) => {
  if (audio.value) {
    const time = (value / 100) * audio.value.duration
    audio.value.currentTime = time
    currentTime.value = time
  }
}

const formatTime = (seconds) => {
  const minutes = Math.floor(seconds / 60)
  const remainingSeconds = Math.floor(seconds % 60)
  return `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`
}

// Role cards data
const roles = [
  {
    title: 'For CEOs and CTOs',
    description: 'Pods are investment-focused, customer-centric organizational blocks that offer end-to-end services. Guide them with your strategic vision and define clear inputs and outputs. Focus on the bigger picture.'
  },
  {
    title: 'For Engineering Managers',
    description: 'Grow engineering excellence within Pods to serve the organization effectively. Guide the Pod as a whole and focus on the bigger picture.'
  },
  {
    title: 'For Product Managers',
    description: 'Guide the Pod with vision and priorities to drive outcomes. Focus on the bigger picture rather than managing individual teams. Focus on the bigger picture.'
  },
  {
    title: 'For Agile Coaches',
    description: 'Experience Pod-based design as the ultimate agile approach, prioritizing interactions over processes. Help create adaptive, result-oriented organizational blocks. Focus on the bigger picture.'
  },
  {
    title: 'For Scrum Masters',
    description: 'Treat the Pod as your Scrum team. Collaborate with other Coaches and Masters to ensure end-to-end ownership and continuous improvement. Focus on the bigger picture.'
  }
]
</script>

<style>
/* Add font imports */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

.v-card {
  transition: all 0.3s ease;
}

.definition-card {
  border: 2px solid #4CAF50 !important;
  border-radius: 0 !important;
  background-color: #f5f8f5 !important;
  box-shadow: none !important;
}

.definition-card::after {
  display: none;
}

.definition-card:hover {
  transform: none;
}

.role-section {
  border-left: 2px solid #4CAF50;
  padding-left: 24px;
}

.role-section h3 {
  color: #212121;
  font-weight: 600;
}

.role-section p {
  color: #616161;
  line-height: 1.6;
  font-size: 1.1rem;
}

/* Apply Poppins to all text */
.v-application {
  font-family: 'Poppins', sans-serif !important;
}

/* Specific styling for titles */
.text-h2 {
  font-family: 'Poppins', sans-serif !important;
  font-weight: 700 !important;
  letter-spacing: -0.5px !important;
}

.text-h4 {
  font-family: 'Poppins', sans-serif !important;
  font-weight: 600 !important;
  letter-spacing: 0 !important;
}

.definition-text {
  white-space: pre-line;
}

.definition-text.font-weight-bold {
  color: #1a1a1a;
}

.definition-text.font-weight-regular {
  color: #2e2e2e;
}

@media (max-width: 960px) {
  .definition-text {
    text-align: left;
    width: 100%;
  }
  
  .definition-card {
    margin-bottom: 48px !important;
  }
  
  .role-section {
    margin-bottom: 32px !important;
  }
}
</style>
