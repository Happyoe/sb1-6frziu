<template>
  <div class="magical-bg p-8 rounded-lg shadow-2xl">
    <h2 class="text-3xl font-bold text-center mb-8 text-yellow-300">Find a Ride</h2>
    <form @submit.prevent="searchRides" class="max-w-md mx-auto bg-purple-800 p-6 rounded-lg shadow-lg">
      <div class="mb-4">
        <label for="from" class="block mb-2">From:</label>
        <input v-model="search.from" id="from" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div class="mb-4">
        <label for="to" class="block mb-2">To:</label>
        <input v-model="search.to" id="to" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div class="mb-4">
        <label for="departure" class="block mb-2">Departure Date:</label>
        <input v-model="search.departure" id="departure" type="date" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <button type="submit" class="w-full bg-green-400 text-purple-900 px-4 py-2 rounded-full font-bold hover:bg-green-300 transition-colors">
        Search Rides
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const search = ref({
  from: '',
  to: '',
  departure: ''
})

const searchRides = () => {
  console.log('Searching for rides:', search.value)
  alert('Searching for available rides...')
  router.push('/')
}
</script>