<!-- src/components/GroupHeader.vue -->
<script setup>
import { useI18n } from 'vue-i18n'
import CountdownTimer from './CountdownTimer.vue'

const props = defineProps({
  reservationNumber: { type: String, required: true },
  departureTime:     { type: String, required: true }
})

const { locale, t } = useI18n()

// Solo la bandera, sin texto, para ahorrar espacio
const langs = [
  { code: 'en', flag: '🇬🇧' },
  { code: 'fr', flag: '🇫🇷' },
  { code: 'nl', flag: '🇳🇱' }
]

function changeLocale(e) {
  locale.value = e.target.value
}
</script>

<template>
  <header
    class="
      fixed inset-x-0 top-0 bg-gradient-to-r from-blue-600 to-blue-500
      z-20 px-4 pt-safe pb-4
      sm:static sm:px-6 sm:py-4
    "
  >
    <div class="max-w-md mx-auto flex flex-col items-center space-y-3">
      <!-- Títulos -->
      <div class="text-center space-y-1">
        <h1 class="text-2xl sm:text-3xl font-bold text-white">
          {{ t('groupTrip') }}
        </h1>
        <p class="text-sm sm:text-base text-white">
          {{ t('subtitle') }}
        </p>
        <p class="text-xs sm:text-sm text-white opacity-80">
          {{ t('reservation', { num: props.reservationNumber }) }}
        </p>
      </div>

      <!-- Pill integrado -->
      <div
        class="
          inline-flex items-center divide-x divide-gray-300
          bg-white rounded-full shadow-md
          overflow-hidden
        "
      >
        <!-- Selector de idioma (fondo blanco) -->
        <div class="flex items-center px-3 py-1">
          <label for="lang" class="sr-only">Language</label>
          <select
            id="lang"
            v-model="locale"
            @change="changeLocale"
            class="
              appearance-none bg-transparent text-lg cursor-pointer
              focus:outline-none text-gray-800
            "
            aria-label="Select language"
          >
            <option
              v-for="l in langs"
              :key="l.code"
              :value="l.code"
            >
              {{ l.flag }}
            </option>
          </select>
          <span class="ml-1 text-gray-600 select-none text-sm">▾</span>
        </div>

        <!-- Countdown compacto -->
        <div class="flex flex-col items-center px-3 py-1">
          <CountdownTimer :departure="props.departureTime" class="text-xs text-black" />
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
/* Respeta notch en iOS */
.pt-safe {
  padding-top: constant(safe-area-inset-top);
  padding-top: env(safe-area-inset-top);
}
</style>
