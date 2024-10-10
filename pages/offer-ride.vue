<template>
  <div>
    <h2 class="text-3xl font-bold text-center mb-8">Offer a Ride</h2>
    <form @submit.prevent="submitRide" class="max-w-md mx-auto bg-purple-800 p-6 rounded-lg shadow-lg">
      <div class="mb-4">
        <label for="from" class="block mb-2">From:</label>
        <input v-model="newRide.from" id="from" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div class="mb-4">
        <label for="to" class="block mb-2">To:</label>
        <input v-model="newRide.to" id="to" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div class="mb-4">
        <label for="departure" class="block mb-2">Departure Time:</label>
        <input v-model="newRide.departure" id="departure" type="time" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div class="mb-4">
        <label for="seats" class="block mb-2">Available Seats:</label>
        <input v-model.number="newRide.seats" id="seats" type="number" min="1" max="10" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <button type="submit" class="w-full bg-yellow-400 text-purple-900 px-4 py-2 rounded font-bold hover:bg-yellow-300 transition-colors">
        Offer Ride
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const newRide = ref({
  from: '',
  to: '',
  departure: '',
  seats: 1
})

const submitRide = () => {
  // Here you would typically send this data to a backend API
  console.log('New ride offered:', newRide.value)
  alert('Your ride has been offered successfully!')
  router.push('/drivers')
}
</script>