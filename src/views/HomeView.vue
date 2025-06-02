<script setup>
import { ref } from 'vue'
import GroupHeader         from '@/components/GroupHeader.vue'
import WelcomeMessage      from '@/components/WelcomeMessage.vue'
import TripSummaryCard     from '@/components/TripSummaryCard.vue'
import GroupSummaryCard    from '@/components/GroupSummaryCard.vue'
import UserInfoCard        from '@/components/UserInfoCard.vue'
import InvoiceInfoCard     from '@/components/InvoiceInfoCard.vue'
import LiveTracking        from '@/components/LiveTracking.vue'
import TravelTipCard       from '@/components/TravelTipCard.vue'
import SharePlatformQR     from '@/components/SharePlatformQR.vue'
import ChatbotWidget       from '@/components/ChatbotWidget.vue'
import PostTripReview      from '@/components/PostTripReview.vue'

const isReviewMode = ref(false)

function handleLeaveFeedback() {
  isReviewMode.value = true
}

function handleBackToTrip() {
  isReviewMode.value = false
}

function handleReviewSubmit(data) {
  console.log('Review submitted:', data)
  // After submit, you could show a thank-you message or reset for demo
}
</script>

<template>
  <main class="pt-48 p-2 sm:pt-0 sm:p-6 relative">
    <div class="w-full space-y-8 px-4">
      <template v-if="!isReviewMode">
        <!-- Header -->
        <GroupHeader reservationNumber="30000 666 0265" />

        <!-- Welcome / Hero section -->
        <WelcomeMessage
          userName="Louis"
          groupName="Chiro Eppegem"
          reservationNumber="30000 666 0265"
        />

        <!-- 2×2 summary grid -->
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
          <TripSummaryCard
            from="Gent-Sint-Pieters"
            to="Antwerpen-Centraal"
            datetime="13/01/25, 12:27"
            train="IC 734"
          />
          <GroupSummaryCard
            :childrenCount="20"
            :teensCount="0"
            :adultsCount="3"
            :childrenPrice="20"
            :teensPrice="0"
            :adultsPrice="18"
            :totalPrice="38"
          />
          <UserInfoCard
            name="Margaux Van Linthoudt"
            organization="Chiro Eppegem"
            phone="+32 474 12 34 56"
            email="margaux@mail.com"
          />
          <InvoiceInfoCard
            organization="Chiro Eppegem vzw"
            address="Adres 123, 4321 Gemeente"
          />
        </div>

        <!-- Live tracking (anchor target) -->
        <div id="live-tracking">
          <LiveTracking />
        </div>

        <!-- QR and Tips side by side -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-6">
          <SharePlatformQR link="https://yourapp.com/group/30000-666-0265" />
          <TravelTipCard
            departureStation="Gent-Sint-Pieters"
            arrivalStation="Antwerp-Central"
            departureIntro="The information below will be completed on the day of departure."
            :departureTips="[
              'Gather with your group 20 minutes in advance.',
              'Use the meeting point at the station entrance.'
            ]"
            :reservedCoach="5"
            :groupSize="23"
            :arrivalTips="[
              'Collect your belongings in time before arrival.',
              'Move your group toward the exit as soon as possible.',
              'We recommend organizing your group starting from Saint-Nicolas station.'
            ]"
            :arrivalDisembarkTips="[
              'Your group includes more than 20 participants. Use both doors when getting off the train.'
            ]"
            :safetyTips="[
              'Keep the group at a safe distance from the tracks.',
              'Always stay behind the line on the platform.',
              'If someone falls onto the tracks, contact SNCB immediately: +32 2 3XX XX XX',
              'Do not board after the train conductor’s signal.'
            ]"
            :emergencyTips="[
              'In case of a strike, check the SNCB website and follow instructions for alternative transport.',
              'If your train is canceled, proceed to the ticket counter or use the SNCB app to rebook.',
              'If reserved seats are occupied, show your reservation confirmation and ask the conductor for assistance.'
            ]"
          />
        </div>

        <!-- Leave feedback button -->
        <div class="mt-8 text-center">
          <button
            @click="handleLeaveFeedback"
            class="bg-blue-600 text-white font-medium py-2 px-6 rounded-md hover:bg-blue-700"
          >
            Leave feedback
          </button>
        </div>
      </template>

      <template v-else>
        <!-- Post-trip review -->
        <PostTripReview @submit="handleReviewSubmit" />

        <!-- Back to trip button -->
        <div class="mt-6 text-center">
          <button
            @click="handleBackToTrip"
            class="bg-gray-200 text-gray-800 font-medium py-2 px-6 rounded-md hover:bg-gray-300"
          >
            Back to trip
          </button>
        </div>
      </template>
    </div>
  </main>
</template>
