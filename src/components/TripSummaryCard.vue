<script setup>
const props = defineProps({
  from: { type: String, required: true },
  to:   { type: String, required: true },
  datetime: { type: String, required: true },
  train: { type: String, required: true },
  onChange: { type: Function, default: null }
})
</script>

<template>
  <div class="border-2 border-dashed border-blue-300 rounded-lg p-6 relative">
    <h2 class="flex justify-between items-center text-lg font-semibold mb-4">
      <span>Je groepsreis</span>
      <button
        @click="onChange"
        class="flex items-center text-blue-600 hover:underline text-sm"
      >
        <!-- icon lápiz -->
        <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5M18.5 2.5a2.121 2.121 0 113 3L12 15l-4 1 1-4 9.5-9.5z"/>
        </svg>
        <span class="ml-1">Wijzig</span>
      </button>
    </h2>
    <div class="flex items-start text-gray-700">
      <!-- icon tren -->
      <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-blue-600 mr-3" fill="none"
           viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M12 2c-3.866 0-7 3.134-7 7v7a5 5 0 005 5h4a5 5 0 005-5V9c0-3.866-3.134-7-7-7z"/>
      </svg>
      <div>
        <p class="font-medium">{{ from }} → {{ to }}</p>
        <p class="text-sm text-gray-500">{{ datetime }} - {{ train }}</p>
      </div>
    </div>
  </div>
</template>
