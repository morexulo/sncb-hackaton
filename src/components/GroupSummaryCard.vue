<script setup>
const props = defineProps({
  childrenCount:   { type: Number, default: 0 },
  teensCount:      { type: Number, default: 0 },
  adultsCount:     { type: Number, default: 0 },
  childrenPrice:   { type: Number, default: 0 },
  teensPrice:      { type: Number, default: 0 },
  adultsPrice:     { type: Number, default: 0 },
  totalPrice:      { type: Number, required: true },
  onChange:        { type: Function, default: null }
})
</script>

<template>
  <div class="border-2 border-dashed border-blue-300 rounded-lg p-6 relative">
    <h2 class="flex justify-between items-center text-lg font-semibold mb-4">
      <span>Je groep</span>
      <button
        @click="onChange"
        class="flex items-center text-blue-600 hover:underline text-sm"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5M18.5 2.5a2.121 2.121 0 113 3L12 15l-4 1 1-4 9.5-9.5z"/>
        </svg>
        <span class="ml-1">Wijzig</span>
      </button>
    </h2>

    <div class="space-y-3 text-gray-700">
      <!-- -12 jaar -->
      <div class="flex justify-between items-center">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-blue-600" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804M15 11a3 3 0 11-6 0
                   3 3 0 016 0z"/>
          </svg>
          <span class="ml-2">-12 jaar</span>
        </div>
        <span>{{ childrenCount }} personen</span>
        <span>€{{ childrenPrice }}</span>
      </div>

      <!-- 12–17 jaar -->
      <div class="flex justify-between items-center text-gray-400">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804
                     M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
          </svg>
          <span class="ml-2">12 –17 jaar</span>
        </div>
        <span>0 personen</span>
        <span>€0</span>
      </div>

      <!-- +18 jaar -->
      <div class="border-t border-gray-300 pt-3 flex justify-between items-center">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-blue-600" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804
                     M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
          </svg>
          <span class="ml-2">+18 jaar</span>
        </div>
        <span>{{ adultsCount }} personen</span>
        <span>€{{ adultsPrice }}</span>
      </div>

      <!-- Total -->
      <div class="text-right font-semibold text-gray-900">
        €{{ totalPrice }}
      </div>
    </div>
  </div>
</template>
