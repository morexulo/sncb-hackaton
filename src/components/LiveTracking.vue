<!-- src/components/LiveTracking.vue -->
<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from 'vue'

// Stops data
const stops = [
  { time: '12:09', station: 'Waregem', subText: '+1', type: 'normal' },
  { time: 'Live location', station: null, type: 'live' },
  {
    time: '12:27',
    station: 'Gent-Sint-Pieters',
    track: '12',
    type: 'station',
    showComposition: true,
  },
  { time: '5 tussenstops', station: null, type: 'intermediate' },
  {
    time: '13:03',
    station: 'Sint-Niklaas',
    type: 'station',
    highlight: 'orange',
    label: 'Maak je klaar om uit te stappen',
  },
  {
    time: '13:23',
    station: 'Antwerpen-Centraal',
    track: '1',
    type: 'station',
  },
]

// Composition data
const composition = {
  wagons: ['2','2','1','2','2','2','2','2'],
  occupancy: 'Expected occupancy: low',
  occupancyLevels: [0.3, 0.5, 0.2, 0.8, 0.4, 0.6, 0.2, 0.3]
}

// Toast notifications
const toasts = ref([])
let toastId = 0
function showToast(msg) {
  const id = toastId++
  toasts.value.push({ id, message: msg })
  setTimeout(() => {
    toasts.value = toasts.value.filter(t => t.id !== id)
  }, 3000)
}

// Geolocation simulation (not real coords)
const userPosition = ref(null)
onMounted(() => {
  // simulate permission granted
  userPosition.value = { latitude: 51.05, longitude: 3.72 }
})

// Automated next-step loop
const currentIndex = ref(0)
function nextStop() {
  currentIndex.value = (currentIndex.value + 1) % stops.length
}
let autoInterval = null
onMounted(() => {
  autoInterval = setInterval(nextStop, 3000)
})
onBeforeUnmount(() => {
  clearInterval(autoInterval)
})

// Compute train icon position
const trainTop = computed(() => {
  const pct = currentIndex.value / (stops.length - 1)
  return `${pct * 100}%`
})
</script>

<template>
  <section class="max-w-4xl mx-auto bg-white p-6 rounded-lg shadow relative">
    <h2 class="text-xl font-semibold mb-4">Follow your train in real time</h2>

    <!-- Toasts -->
    <div class="fixed top-6 right-6 space-y-2 z-50">
      <div
        v-for="t in toasts"
        :key="t.id"
        class="bg-gray-800 text-white px-4 py-2 rounded shadow"
      >
        {{ t.message }}
      </div>
    </div>

    <!-- Simulated location -->
    <div v-if="userPosition" class="mb-4 text-sm text-gray-600">
      Your location: Track 12 at Gent-Sint-Pieters.
    </div>

    <div class="relative pl-8">
      <!-- Vertical line -->
      <div class="absolute left-3 top-0 bottom-0 w-px bg-blue-600"></div>

      <!-- Animated train icon -->
      <div
        class="absolute left-0 w-6 h-6 -ml-3 transition-all duration-3000 ease-linear"
        :style="{ top: trainTop, transitionProperty: 'top, left' }"
      >
        <img src="/train.png" alt="Train" class="w-full h-full" />
      </div>

      <ul class="space-y-12">
        <li v-for="(stop, i) in stops" :key="i" class="relative">
          <!-- Marker circle -->
          <div
            :class="[
              'absolute -left-1.5 w-3 h-3 rounded-full border-2 transition-colors duration-500',
              stop.type==='live'         ? 'bg-white border-blue-600' :
              stop.type==='intermediate' ? 'bg-white border-gray-300' :
              stop.highlight==='orange'  ? 'bg-orange-500 border-orange-500' :
                                           'bg-blue-600 border-blue-600'
            ]"
          ></div>

          <div class="ml-6 space-y-1">
            <!-- Time -->
            <div class="flex items-baseline space-x-3">
              <span class="font-medium">{{ stop.time }}</span>
              <span v-if="stop.subText" class="text-sm text-red-600">{{ stop.subText }}</span>
            </div>

            <!-- Live location -->
            <div v-if="stop.type==='live'" class="flex items-center text-blue-600 font-medium">
              <img src="/train.png" alt="Live" class="w-5 h-5 mr-2" />
              <span>Live location</span>
            </div>

            <!-- Station label -->
            <div v-else-if="stop.type==='station' && !stop.showComposition && !stop.highlight">
              <p class="font-medium">
                {{ stop.station }}<span v-if="stop.track"> spoor {{ stop.track }}</span>
              </p>
            </div>

            <!-- Composition -->
            <div v-else-if="stop.showComposition" class="space-y-3">
              <p class="font-medium">{{ stop.station }} spoor {{ stop.track }}</p>
              <div class="bg-white p-3 rounded-lg shadow-sm">
                <!-- Wagons + connector -->
                <div class="relative flex items-center justify-between w-full">
                  <div class="absolute inset-y-1/2 left-0 right-0 h-px bg-gray-300 z-0"></div>
                  <div
                    v-for="(w, wi) in composition.wagons"
                    :key="wi"
                    class="flex-shrink-0 w-6 h-6 bg-blue-600 text-white flex items-center justify-center text-xs rounded z-10"
                  >
                    {{ w }}
                  </div>
                </div>
                <!-- Occupancy bar chart -->
                <div class="mt-3 flex items-end space-x-1 h-16">
                  <div
                    v-for="(lvl, idx) in composition.occupancyLevels"
                    :key="idx"
                    class="flex-1 bg-blue-200"
                    :style="{ height: `${lvl * 100}%` }"
                  ></div>
                </div>
                <div class="mt-2 text-sm text-green-800">{{ composition.occupancy }}</div>
              </div>
            </div>

            <!-- Intermediate -->
            <div v-else-if="stop.type==='intermediate'" class="text-gray-500 italic">
              {{ stop.time }}
            </div>

            <!-- Highlight -->
            <div v-else-if="stop.highlight==='orange'" class="flex items-center space-x-2">
              <p class="font-medium">{{ stop.station }}</p>
              <img src="/train.png" alt="Highlight" class="w-4 h-4 rotate-45 text-gray-600" />
              <span class="text-gray-600 text-sm">{{ stop.label }}</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>
