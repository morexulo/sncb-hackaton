<!-- src/components/WelcomeMessage.vue -->
<script setup>
import { ref, onMounted } from 'vue'

const props = defineProps({
  userName: {
    type: String,
    default: 'Traveler'
  },
  groupName: {
    type: String,
    default: ''
  },
  reservationNumber: {
    type: String,
    default: ''
  }
})

// for simple fade-in on mount
const isVisible = ref(false)
onMounted(() => {
  setTimeout(() => isVisible.value = true, 50)
})
</script>

<template>
  <section class="relative max-w-4xl mx-auto overflow-hidden  shadow-lg">
    <!-- Hero background with gradient overlay -->
    <div class="relative h-64 sm:h-80">
      <img
        src="/welcome.png"
        alt="Train hero"
        class="absolute inset-0 w-full h-full object-cover object-center transition-transform duration-700 ease-out hover:scale-105"
      />
      <div class="absolute inset-0 bg-gradient-to-b from-black/40 to-black/10"></div>
      <!-- Overlay text -->
      <div
        class="absolute inset-0 flex flex-col justify-center items-center px-6 text-center text-white space-y-3 transition-opacity duration-700"
        :class="isVisible ? 'opacity-100' : 'opacity-0'"
      >
        <h2 class="text-2xl sm:text-3xl font-bold">
          Hello {{ userName }}<span v-if="groupName"> of {{ groupName }}</span>!
        </h2>
        <p class="text-sm sm:text-base max-w-md">
          Thank you for booking your group trip.<br />
          Reservation #<span class="font-medium">{{ reservationNumber }}</span>
        </p>
      </div>
    </div>

    <!-- Body content -->
    <div class="bg-white p-6 space-y-4">
      <p class="text-gray-800 text-lg font-semibold">
        We’re excited to welcome you on board
      </p>
      <p class="text-gray-700 leading-relaxed">
        Below you’ll find all the tips and tools you need for a smooth journey.
        Feel free to explore your itinerary, track the train in real time, and
        adjust your details at any time.
      </p>
      <!-- CTA button -->
      <div class="text-center">
        <a
          href="#live-tracking"
          class="inline-block px-5 py-2 bg-blue-600 text-white font-medium rounded-lg shadow hover:bg-blue-700 transition"
        >
          View your journey →
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* nothing extra—Tailwind handles transitions */
</style>
