<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { useI18n } from 'vue-i18n'
import dayjs from 'dayjs'

const { t } = useI18n()

// Siempre +1h y se resetea al llegar a 3min
const departureTime = ref(dayjs().add(1, 'hour'))
const remaining     = ref('01:00:00')
let timer = null

function update() {
  const now = dayjs()
  let diff = departureTime.value.diff(now)

  if (diff <= 3 * 60 * 1000) {
    departureTime.value = dayjs().add(1, 'hour')
    diff = departureTime.value.diff(now)
  }

  const hrs  = Math.floor(diff / 3_600_000)
  const mins = Math.floor((diff % 3_600_000) / 60_000)
  const secs = Math.floor((diff % 60_000) / 1000)

  remaining.value =
    String(hrs).padStart(2,'0') + ':' +
    String(mins).padStart(2,'0') + ':' +
    String(secs).padStart(2,'0')
}

onMounted(() => {
  update()
  timer = setInterval(update, 1000)
})
onBeforeUnmount(() => clearInterval(timer))
</script>

<template>
  <div class="flex flex-col items-center">
    <span class="text-xs font-medium text-black">
      {{ t('timeToDeparture') }}
    </span>
    <span class="mt-0.5 text-sm font-bold text-black">
      {{ remaining }}
    </span>
  </div>
</template>

<style scoped>
/* eliminamos blur y fondo: lo pinta el pill externo */
</style>
