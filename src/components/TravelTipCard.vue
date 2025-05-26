<!-- src/components/TravelTipCard.vue -->
<script setup>
import { computed } from 'vue'

const props = defineProps({
  station: {
    type: String,
    required: true
  },
  type: {
    type: String,
    default: 'departure' // or 'arrival'
  },
  reservedCoach: {
    type: [String, Number],
    default: ''
  },
  tips: {
    type: Array,
    default: () => []
  },
  warnings: {
    type: Array,
    default: () => []
  },
  infoLink: {
    type: String,
    default: '#'
  }
})

const typeLabel = computed(() => {
  return props.type === 'arrival' ? 'Arrival' : 'Departure'
})
</script>

<template>
  <div class="max-w-md bg-white p-4 rounded-lg shadow flex flex-col space-y-4">
    <!-- Header -->
    <div class="flex items-center justify-between">
      <div class="flex items-center space-x-2">
        <!-- Train icon -->
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-blue-600" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M12 2c-3.866 0-7 3.134-7 7v7a5 5 0 005
                   5h4a5 5 0 005-5V9c0-3.866-3.134-7-7-7z"/>
        </svg>
        <h3 class="text-lg font-semibold text-gray-900">{{ station }}</h3>
        <span
          class="ml-2 px-2 py-0.5 text-xs font-medium text-white bg-blue-600 rounded"
        >
          {{ typeLabel }}
        </span>
      </div>
      <a
        :href="infoLink"
        class="text-sm text-blue-600 hover:underline"
      >
        More info
      </a>
    </div>

    <!-- Tips list -->
    <ul v-if="tips.length" class="space-y-1">
      <li
        v-for="(tip, idx) in tips"
        :key="idx"
        class="flex items-start"
      >
        <div class="w-2 h-2 bg-blue-600 rounded-full mt-1 mr-2"></div>
        <p class="text-gray-700 text-sm">{{ tip }}</p>
      </li>
    </ul>

    <!-- Warnings list -->
    <ul v-if="warnings.length" class="space-y-1">
      <li
        v-for="(warn, idx) in warnings"
        :key="idx"
        class="flex items-start"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-red-600 mt-1 mr-2" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54
                   0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464
                   0L3.34 16c-.77 1.333.192 3 1.732 3z"/>
        </svg>
        <p class="text-red-600 text-sm">{{ warn }}</p>
      </li>
    </ul>

    <!-- Reserved coach -->
    <div class="flex items-center space-x-2">
      <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-gray-500" fill="none"
           viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M3 13h2l1 2h8l1-2h2m-1-5h-2l-1-2H8l-1 2H5m-1
                 5h16m-5 5h-6m-4 0a2 2 0 11-4 0 2 2 0 014 0zm12
                 0a2 2 0 11-4 0 2 2 0 014 0z"/>
      </svg>
      <span class="text-gray-700 text-sm">
        Reserved coach: <span class="font-medium">{{ reservedCoach }}</span>
      </span>
    </div>
  </div>
</template>
