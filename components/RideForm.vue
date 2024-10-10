<template>
  <div class="max-w-md mx-auto bg-purple-800 p-6 rounded-lg shadow-lg">
    <div class="flex justify-center mb-6">
      <button 
        @click="isDriver = false" 
        :class="['px-4 py-2 rounded-l-full font-bold transition-colors', 
                 !isDriver ? 'bg-yellow-400 text-purple-900' : 'bg-purple-700 text-white']"
      >
        <i class="fas fa-user mr-2"></i> Passenger
      </button>
      <button 
        @click="isDriver = true" 
        :class="['px-4 py-2 rounded-r-full font-bold transition-colors', 
                 isDriver ? 'bg-yellow-400 text-purple-900' : 'bg-purple-700 text-white']"
      >
        <i class="fas fa-car mr-2"></i> Driver
      </button>
    </div>
    <form @submit.prevent="submitRide" class="space-y-4">
      <div>
        <label for="from" class="block mb-2">From:</label>
        <input v-model="ride.from" id="from" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div>
        <label for="to" class="block mb-2">To:</label>
        <input v-model="ride.to" id="to" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div>
        <label for="departure" class="block mb-2">Departure Time:</label>
        <input v-model="ride.departure" id="departure" type="datetime-local" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <div v-if="isDriver">
        <label for="seats" class="block mb-2">Available Seats:</label>
        <input v-model.number="ride.seats" id="seats" type="number" min="1" max="10" required class="w-full px-3 py-2 text-purple-900 rounded">
      </div>
      <button type="submit" class="w-full bg-yellow-400 text-purple-900 px-4 py-2 rounded-full font-bold hover:bg-yellow-300 transition-colors transform hover:scale-105">
        {{ isDriver ? 'Offer Ride' : 'Find Rides' }}
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const isDriver = ref(false)

const ride = ref({
  from: '',
  to: '',
  departure: '',
  seats: 1
})

const submitRide = () => {
  if (isDriver.value) {
    console.log('New ride offered:', ride.value)
    alert('Your ride has been offered successfully!')
  } else {
    console.log('Searching for rides:', ride.value)
    alert('Searching for available rides...')
  }
  router.push('/')
}
</script>