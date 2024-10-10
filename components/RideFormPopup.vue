<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-purple-800 p-6 rounded-lg shadow-lg max-w-md w-full">
      <h2 class="text-2xl font-bold mb-4 text-yellow-300">{{ isDriver ? 'Add a Ride' : 'Request a Lift' }}</h2>
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
        <div>
          <label for="phone" class="block mb-2">Phone Number:</label>
          <div class="flex">
            <span class="bg-gray-200 text-gray-700 px-3 py-2 rounded-l">+972</span>
            <input v-model="ride.phone" id="phone" type="tel" required pattern="^0?\d{9}$" class="flex-grow px-3 py-2 text-purple-900 rounded-r" placeholder="e.g., 0501234567">
          </div>
        </div>
        <div class="flex justify-end space-x-4">
          <button @click="$emit('close')" type="button" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-full">Cancel</button>
          <button type="submit" class="px-4 py-2 bg-yellow-400 text-purple-900 rounded-full font-bold hover:bg-yellow-300 transition-colors">
            {{ isDriver ? 'Add Ride' : 'Find Rides' }}
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  isDriver: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['close'])

const ride = ref({
  from: '',
  to: '',
  departure: '',
  seats: 1,
  phone: ''
})

const submitRide = () => {
  const formattedPhone = formatPhoneNumber(ride.value.phone)
  if (props.isDriver) {
    console.log('New ride offered:', { ...ride.value, phone: formattedPhone })
    alert('Your ride has been offered successfully!')
  } else {
    console.log('Searching for rides:', { ...ride.value, phone: formattedPhone })
    alert('Searching for available rides...')
  }
  emit('close')
}

const formatPhoneNumber = (phone) => {
  const cleaned = phone.replace(/\D/g, '')
  return cleaned.startsWith('0') ? `+972${cleaned.slice(1)}` : `+972${cleaned}`
}
</script>