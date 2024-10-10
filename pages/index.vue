<template>
  <div class="magical-bg p-8 rounded-lg shadow-2xl">
    <h1 class="text-5xl font-bold mb-8 text-center text-yellow-300">Welcome to Creator Magic</h1>
    <p class="text-xl mb-8 text-center">Connect with fellow creators and share magical rides!</p>
    
    <div class="flex justify-center mb-8">
      <button 
        @click="setActiveTab('passenger')" 
        :class="['px-6 py-3 rounded-l-full font-bold transition-colors', 
                 activeTab === 'passenger' ? 'bg-yellow-400 text-purple-900' : 'bg-purple-700 text-white']"
      >
        <i class="fas fa-user mr-2"></i> Passenger
      </button>
      <button 
        @click="setActiveTab('driver')" 
        :class="['px-6 py-3 rounded-r-full font-bold transition-colors', 
                 activeTab === 'driver' ? 'bg-yellow-400 text-purple-900' : 'bg-purple-700 text-white']"
      >
        <i class="fas fa-car mr-2"></i> Driver
      </button>
    </div>
    
    <div class="bg-purple-800 p-6 rounded-lg shadow-lg">
      <div class="flex justify-between items-center mb-6">
        <h2 class="text-3xl font-bold text-yellow-300">
          {{ activeTab === 'passenger' ? 'Available Rides' : 'Your Offered Rides' }}
        </h2>
        <div class="relative">
          <input 
            v-model="searchTerm" 
            type="text" 
            placeholder="Search rides..." 
            class="px-4 py-2 rounded-full bg-purple-700 text-white placeholder-purple-300 focus:outline-none focus:ring-2 focus:ring-yellow-400"
          >
          <i class="fas fa-search absolute right-3 top-1/2 transform -translate-y-1/2 text-purple-300"></i>
        </div>
      </div>
      <RideList 
        :rides="filteredRides" 
        :type="activeTab" 
        @edit-ride="editRide"
      />
    </div>
  </div>
  <EditRideModal v-if="showEditModal" :ride="selectedRide" @close="closeEditModal" @save="saveEditedRide" />
</template>

<script setup>
import { ref, computed } from 'vue'
import RideList from '~/components/RideList.vue'
import EditRideModal from '~/components/EditRideModal.vue'

const activeTab = ref('passenger')
const searchTerm = ref('')
const showEditModal = ref(false)
const selectedRide = ref(null)

const generateRandomPhone = () => {
  const areaCode = '+972'
  const number = Math.floor(Math.random() * 1000000000).toString().padStart(9, '0')
  return `${areaCode}${number}`
}

const generateRides = (count, isOffered = false) => {
  return Array.from({ length: count }, (_, i) => ({
    id: i + 1,
    driver: `Driver ${i + 1}`,
    from: `Location ${i + 1}`,
    to: `Destination ${i + 1}`,
    departure: new Date(Date.now() + Math.random() * 7 * 24 * 60 * 60 * 1000).toLocaleString(),
    seats: Math.floor(Math.random() * 4) + 1,
    phone: generateRandomPhone(),
    isAdmin: i === 0
  }))
}

const availableRides = ref(generateRides(6))
const offeredRides = ref(generateRides(4, true))

const filteredRides = computed(() => {
  const rides = activeTab.value === 'passenger' ? availableRides.value : offeredRides.value
  if (!searchTerm.value) return rides
  const lowercasedTerm = searchTerm.value.toLowerCase()
  return rides.filter(ride => 
    ride.driver.toLowerCase().includes(lowercasedTerm) ||
    ride.from.toLowerCase().includes(lowercasedTerm) ||
    ride.to.toLowerCase().includes(lowercasedTerm)
  )
})

const emit = defineEmits(['toggle-mode'])

const setActiveTab = (tab) => {
  activeTab.value = tab
  emit('toggle-mode', tab)
}

const editRide = (ride) => {
  selectedRide.value = { ...ride }
  showEditModal.value = true
}

const closeEditModal = () => {
  showEditModal.value = false
  selectedRide.value = null
}

const saveEditedRide = (editedRide) => {
  const rides = activeTab.value === 'passenger' ? availableRides : offeredRides
  const index = rides.value.findIndex(r => r.id === editedRide.id)
  if (index !== -1) {
    rides.value[index] = editedRide
  }
  closeEditModal()
}
</script>