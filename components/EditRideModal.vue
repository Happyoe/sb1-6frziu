<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-purple-800 p-6 rounded-lg shadow-lg max-w-md w-full">
      <h2 class="text-2xl font-bold mb-4 text-yellow-300">Edit Ride</h2>
      <form @submit.prevent="confirmEdit" class="space-y-4">
        <div>
          <label for="from" class="block mb-2">From:</label>
          <input v-model="editedRide.from" id="from" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
        </div>
        <div>
          <label for="to" class="block mb-2">To:</label>
          <input v-model="editedRide.to" id="to" type="text" required class="w-full px-3 py-2 text-purple-900 rounded">
        </div>
        <div>
          <label for="departure" class="block mb-2">Departure Time:</label>
          <input v-model="editedRide.departure" id="departure" type="datetime-local" required class="w-full px-3 py-2 text-purple-900 rounded">
        </div>
        <div>
          <label for="seats" class="block mb-2">Available Seats:</label>
          <input v-model.number="editedRide.seats" id="seats" type="number" min="1" max="10" required class="w-full px-3 py-2 text-purple-900 rounded">
        </div>
        <div class="flex justify-end space-x-4">
          <button @click="$emit('close')" type="button" class="px-4 py-2 bg-gray-300 text-gray-800 rounded-full">Cancel</button>
          <button type="submit" class="px-4 py-2 bg-yellow-400 text-purple-900 rounded-full font-bold hover:bg-yellow-300 transition-colors">
            Save Changes
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  ride: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['close', 'save'])

const editedRide = ref({ ...props.ride })

const confirmEdit = () => {
  if (confirm('Are you sure you want to save these changes?')) {
    emit('save', editedRide.value)
  }
}
</script>