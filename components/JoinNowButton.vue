<template>
  <button class="join-now-btn px-8 py-4 bg-yellow-400 text-purple-900 font-bold rounded-full text-xl shadow-lg transition-all duration-300 hover:bg-yellow-300 hover:scale-105">
    Join Now
  </button>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'

let tl

onMounted(() => {
  tl = gsap.timeline({ repeat: -1, yoyo: true })
  tl.to('.join-now-btn', { duration: 0.5, scale: 1.1, boxShadow: '0 0 20px rgba(255, 255, 0, 0.7)' })
    .to('.join-now-btn', { duration: 0.5, scale: 1, boxShadow: '0 0 0px rgba(255, 255, 0, 0)' })
})

onUnmounted(() => {
  if (tl) tl.kill()
})
</script>

<style scoped>
.join-now-btn {
  transition: all 0.3s ease;
}

.join-now-btn:hover {
  animation: pulse 1s infinite;
}

@keyframes pulse {
  0% { box-shadow: 0 0 0 0 rgba(255, 255, 0, 0.7); }
  70% { box-shadow: 0 0 0 15px rgba(255, 255, 0, 0); }
  100% { box-shadow: 0 0 0 0 rgba(255, 255, 0, 0); }
}
</style>