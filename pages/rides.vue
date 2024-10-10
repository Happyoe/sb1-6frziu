<template>
  <div class="magical-bg p-8 rounded-lg shadow-2xl">
    <h2 class="text-3xl font-bold text-center mb-8">{{ activeTab === 'driver' ? 'Your Offered Rides' : 'Available Rides' }}</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div v-for="ride in rides" :key="ride.id" class="bg-purple-800 p-6 rounded-lg shadow-lg transform hover:scale-105 transition-transform">
        <h3 class="text-2xl font-bold mb-2">{{ ride.driver }}</h3>
        <p><strong>From:</strong> {{ ride.from }}</p>
        <p><strong>To:</strong> {{ ride.to }}</p>
        <p><strong>Departure:</strong> {{ ride.departure }}</p>
        <p><strong>Available Seats:</strong> {{ ride.seats }}</p>
        <button v-if="activeTab === 'passenger'" @click="bookRide(ride.id)" class="mt-4 bg-yellow-400 text-purple-900 px-4 py-2 rounded-full font-bold hover:bg-yellow-300 transition-colors">
          Book Ride
        </button>
        <button v-else @click="editRide(ride.id)" class="mt-4 bg-yellow-400 text-purple-900 px-4 py-2 rounded-full font-bold hover:bg-yellow-300 transition-colors">
          Edit Ride
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps(['activeTab'])

const rides = ref([
  { id: 1, driver: "Alice Wonder", from: "Magic Square", to: "Enchanted Forest", departure: "10:00 AM", seats: 3 },
  { id: 2, driver: "Bob Wizard", from: "Enchanted Avenue", to: "Mystic Mountain", departure: "11:30 AM", seats: 2 },
  { id: 3, driver: "Charlie Spellcaster", from: "Mystic Park", to: "Sorcerer's Summit", departure: "1:00 PM", seats: 4 },
  { id: 4, driver: "Diana Enchantress", from: "Sorcerer's Lane", to: "Wizard's Alley", departure: "2:30 PM", seats: 1 },
  { id: 5, driver: "Ethan Magician", from: "Illusion Street", to: "Potion Plaza", departure: "4:00 PM", seats: 3 },
  { id: 6, driver: "Fiona Charmer", from: "Wand Way", to: "Spell Square", departure: "5:30 PM", seats: 2 },
])

const bookRide = (rideId) => {
  const ride = rides.value.find(r => r.id === rideId)
  if (ride && ride.seats > 0) {
    ride.seats--
    alert(`Ride booked with ${ride.driver}! ${ride.seats} seats remaining.`)
  } else {
    alert("Sorry, this ride is fully booked.")
  }
}

const editRide = (rideId) => {
  alert(`Editing ride ${rideId}. This feature is not yet implemented.`)
}
</script>