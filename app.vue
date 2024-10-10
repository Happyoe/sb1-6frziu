<template>
  <div class="min-h-screen bg-gradient-to-br from-purple-900 to-indigo-900 text-white">
    <header class="bg-purple-800 p-4 shadow-lg">
      <nav class="container mx-auto flex justify-between items-center">
        <NuxtLink to="/" class="text-3xl font-bold text-yellow-300">Creator Magic</NuxtLink>
        <button @click="showForm = true" class="bg-yellow-400 text-purple-900 px-6 py-2 rounded-full font-bold hover:bg-yellow-300 transition-colors">
          {{ isDriver ? 'Add a ride' : 'Request a lift' }}
        </button>
      </nav>
    </header>
    <main class="container mx-auto px-4 py-8">
      <NuxtPage @toggle-mode="toggleMode" />
    </main>
    <RideFormPopup v-if="showForm" @close="showForm = false" :isDriver="isDriver" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toastification'

const showForm = ref(false)
const isDriver = ref(false)
const toast = useToast()

const toggleMode = (mode) => {
  isDriver.value = mode === 'driver'
}

// Add this to show tooltips
const vTooltip = {
  mounted(el, binding) {
    el.setAttribute('data-tooltip', binding.value)
    el.classList.add('tooltip')
  }
}
</script>

<style>
@import 'vue-toastification/dist/index.css';

body {
  @apply bg-purple-900;
}

.magical-bg {
  background-image: url('data:image/svg+xml;charset=utf8,%3Csvg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"%3E%3Cpath fill="%234B0082" fill-opacity="0.2" d="M0,32L48,80C96,128,192,224,288,224C384,224,480,128,576,90.7C672,53,768,75,864,96C960,117,1056,139,1152,149.3C1248,160,1344,160,1392,160L1440,160L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"%3E%3C/path%3E%3C/svg%3E');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.tooltip {
  position: relative;
}

.tooltip::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background-color: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s, visibility 0.3s;
}

.tooltip:hover::after {
  opacity: 1;
  visibility: visible;
}
</style>