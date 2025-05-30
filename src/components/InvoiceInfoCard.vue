<script setup>
import { defineProps } from 'vue'
import { useI18n } from 'vue-i18n'

const props = defineProps({
  organization: { type: String, required: true },
  address:      { type: String, required: true },
  onChange:     { type: Function, default: null }
})

const { t } = useI18n()
</script>

<template>
  <div class="bg-blue-600 text-white rounded-lg p-4 sm:p-6">
    <!-- Header -->
    <h2
      class="flex flex-col sm:flex-row justify-between items-start sm:items-center
             text-lg font-semibold mb-4"
    >
      <span>{{ t('invoice.title') }}</span>
      <button
        @click="onChange"
        class="mt-2 sm:mt-0 flex items-center text-white/80 hover:text-white text-sm"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 sm:w-4 sm:h-4 mr-1" fill="none"
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5
                   M18.5 2.5a2.121 2.121 0 113 3L12 15l-4 1 1-4 9.5-9.5z"/>
        </svg>
        {{ t('common.modify') }}
      </button>
    </h2>

    <!-- Invoice info list -->
    <ul class="space-y-4 text-sm sm:text-base">
      <!-- Organization -->
      <li class="flex flex-col sm:flex-row sm:justify-between sm:items-center">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 sm:w-5 sm:h-5" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M5.121 17.804A13.937 13.937 0 0112 15c2.684 0 5.198.828 7.121 2.804
                     M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>
          </svg>
          <span class="ml-3">{{ props.organization }}</span>
        </div>
      </li>

      <!-- Address -->
      <li class="flex flex-col sm:flex-row sm:justify-between sm:items-center">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 sm:w-5 sm:h-5" fill="none"
               viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M4 5h16M4 9h16M4 13h16M4 17h16"/>
          </svg>
          <span class="ml-3">{{ props.address }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>
