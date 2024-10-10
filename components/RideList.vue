<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    <div v-for="ride in rides" :key="ride.id" class="bg-purple-700 p-6 rounded-lg shadow transition-transform hover:scale-105">
      <h3 class="text-xl font-bold mb-4">{{ ride.driver }}</h3>
      <p class="mb-2"><strong>From:</strong> {{ ride.from }}</p>
      <p class="mb-2"><strong>To:</strong> {{ ride.to }}</p>
      <p class="mb-2"><strong>Departure:</strong> {{ ride.departure }}</p>
      <p class="mb-4"><strong>Available Seats:</strong> {{ ride.seats }}</p>
      <div class="flex flex-wrap gap-2">
        <a :href="getWhatsAppLink(ride.phone)" target="_blank" rel="noopener noreferrer" class="flex-grow bg-green-500 text-white px-4 py-2 rounded-full font-bold hover:bg-green-600 transition-colors text-center">
          <i class="fab fa-whatsapp mr-2"></i> WhatsApp
        </a>
        <button 
          v-if="type === 'driver' && ride.isAdmin"
          @click="$emit('edit-ride', ride)" 
          class="flex-grow bg-yellow-400 text-purple-900 px-4 py-2 rounded-full font-bold hover:bg-yellow-300 transition-colors"
          v-tooltip="'Edit this ride'"
        >
          <i class="fas fa-edit mr-2"></i> Edit
        </button>
        <button 
          v-if="type === 'passenger'"
          @click="bookRide(ride.id)" 
          class="flex-grow bg-yellow-400 text-purple-900 px-4 py-2 rounded-full font-bold hover:bg-yellow-300 transition-colors"
        >
          <i class="fas fa-ticket-alt mr-2"></i> Book
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  rides: {
    type: Array,
    required: true
  },
  type: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['edit-ride'])

const getWhatsAppLink = (phone) => {
  const formattedPhone = phone.startsWith('+') ? phone.slice(1) : phone
  return `https://wa.me/${formattedPhone}`
}

const bookRide = (rideId) => {
  alert(`Booking ride ${rideId}. This feature is not yet implemented.`)
}
</script>