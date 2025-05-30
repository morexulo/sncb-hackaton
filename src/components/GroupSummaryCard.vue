<script setup>
import { defineProps } from 'vue'
import { useI18n } from 'vue-i18n'

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

const { t } = useI18n()
</script>

<template>
  <div class="border-2 border-dashed border-blue-300 rounded-lg p-4 sm:p-6 relative bg-white">
    <h2
      class="flex flex-col sm:flex-row justify-between items-start sm:items-center text-lg font-semibold mb-4"
    >
      <span>{{ t('groupSummary.title') }}</span>
      <button
        @click="onChange"
        class="mt-2 sm:mt-0 flex items-center text-blue-600 hover:underline text-sm"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 sm:w-4 sm:h-4" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5
                   M18.5 2.5a2.121 2.121 0 113 3L12 15l-4 1 1-4 9.5-9.5z"/>
        </svg>
        <span class="ml-1">{{ t('common.modify') }}</span>
      </button>
    </h2>

    <div class="space-y-4 text-gray-700">
      <!-- Under 12 years -->
      <div class="flex flex-col sm:flex-row sm:justify-between sm:items-center">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 sm:w-5 sm:h-5 text-blue-600" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804
                     M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
          </svg>
          <span class="ml-2 text-sm sm:text-base">{{ t('groupSummary.under12') }}</span>
        </div>
        <div class="mt-2 sm:mt-0 flex justify-between sm:justify-end space-x-4 text-sm sm:text-base">
          <span>{{ childrenCount }} {{ t('common.people') }}</span>
          <span>€{{ childrenPrice }}</span>
        </div>
      </div>

      <!-- 12–17 years -->
      <div class="flex flex-col sm:flex-row sm:justify-between sm:items-center">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 sm:w-5 sm:h-5 text-gray-400" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804
                     M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
          </svg>
          <span class="ml-2 text-sm sm:text-base">{{ t('groupSummary.teens') }}</span>
        </div>
        <div class="mt-2 sm:mt-0 flex justify-between sm:justify-end space-x-4 text-sm sm:text-base">
          <span>{{ teensCount }} {{ t('common.people') }}</span>
          <span>€{{ teensPrice }}</span>
        </div>
      </div>

      <!-- 18 years and older -->
      <div class="flex flex-col sm:flex-row sm:justify-between sm:items-center border-t border-gray-300 pt-3">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 sm:w-5 sm:h-5 text-blue-600" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804
                     M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
          </svg>
          <span class="ml-2 text-sm sm:text-base">{{ t('groupSummary.adults') }}</span>
        </div>
        <div class="mt-2 sm:mt-0 flex justify-between sm:justify-end space-x-4 text-sm sm:text-base">
          <span>{{ adultsCount }} {{ t('common.people') }}</span>
          <span>€{{ adultsPrice }}</span>
        </div>
      </div>

      <!-- Total -->
      <div class="text-right font-semibold text-gray-900 text-base sm:text-lg">
        €{{ totalPrice }}
      </div>
    </div>
  </div>
</template>
