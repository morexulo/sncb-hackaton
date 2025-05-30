<!-- src/components/PostTripReview.vue -->
<script setup>
import { ref } from 'vue'

const ratingPunctuality = ref(0)
const ratingOrientation = ref(0)
const comment = ref('')
const isSubmitting = ref(false)

const emit = defineEmits(['submit'])

function handleSubmit() {
  isSubmitting.value = true
  // simulate API call
  setTimeout(() => {
    emit('submit', {
      punctuality: ratingPunctuality.value,
      orientation: ratingOrientation.value,
      comment: comment.value,
    })
    isSubmitting.value = false
    // reset
    ratingPunctuality.value = 0
    ratingOrientation.value = 0
    comment.value = ''
  }, 500)
}
</script>

<template>
  <div class="max-w-md mx-auto bg-white rounded-lg shadow p-6 space-y-6">
    <!-- Header -->
    <h2 class="text-xl font-semibold text-gray-800 text-center">How was your trip?</h2>

    <!-- Punctuality Rating -->
    <div class="space-y-2">
      <label class="block text-gray-700 font-medium"> How would you rate your journey? </label>
      <div class="flex justify-between">
        <button
          v-for="n in 5"
          :key="'punc-' + n"
          @click="ratingPunctuality = n"
          :class="['text-2xl', ratingPunctuality >= n ? 'text-yellow-400' : 'text-gray-300']"
          aria-label="Rate punctuality"
        >
          ★
        </button>
      </div>
    </div>

    <!-- Orientation Rating -->
    <div class="space-y-2">
      <label class="block text-gray-700 font-medium">
        Was it easy to find your seats and platform?
      </label>
      <div class="flex justify-between">
        <button
          v-for="n in 5"
          :key="'orient-' + n"
          @click="ratingOrientation = n"
          :class="['text-2xl', ratingOrientation >= n ? 'text-green-400' : 'text-gray-300']"
          aria-label="Rate orientation"
        >
          ★
        </button>
      </div>
    </div>

    <!-- Optional Comment -->
    <div class="space-y-2">
      <label for="comment" class="block text-gray-700 font-medium">
        Anything else you'd like to share?
      </label>
      <textarea
        id="comment"
        v-model="comment"
        rows="3"
        class="w-full border rounded-md p-2 text-gray-700 focus:ring focus:ring-blue-200"
        placeholder="Your comments (optional)"
      ></textarea>
    </div>

    <!-- Time Indicator -->
    <p class="text-sm text-gray-500 text-center">Takes less than 30 seconds!</p>

    <!-- Submit Button -->
    <button
      @click="handleSubmit"
      :disabled="isSubmitting"
      class="w-full bg-blue-600 text-white font-medium py-2 rounded-md hover:bg-blue-700 disabled:opacity-50"
    >
      {{ isSubmitting ? 'Submitting...' : 'Submit feedback' }}
    </button>
  </div>
</template>

<style scoped>
button:focus {
  outline: none;
  box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.5);
}
</style>
