<script setup>
defineProps({
  reservationNumber: {
    type: String,
    required: true
  }
})
</script>

<template>
  <header class="flex flex-col md:flex-row items-start md:items-center justify-between bg-white py-6 px-4 md:px-8 border-b">
    <!-- Left: title & subtitles -->
    <div class="space-y-1">
      <h1 class="text-2xl font-bold text-gray-900">Group trip</h1>
      <p class="text-gray-700">All information about your group trip by train</p>
      <p class="text-sm text-gray-500">Resv. no. {{ reservationNumber }}</p>
    </div>

    <!-- Right: change button -->
    <button
      type="button"
      class="mt-4 md:mt-0 bg-orange-500 hover:bg-orange-600 text-white font-medium py-2 px-4 rounded"
    >
      Change reservation
    </button>
  </header>
</template>
