<!-- src/views/GroupReservationView.vue -->
<script setup>
import GroupHeader         from '@/components/GroupHeader.vue'
import WelcomeMessage      from '@/components/WelcomeMessage.vue'
import TrainLineProgress   from '@/components/TrainLineProgress.vue'
import TripSummaryCard     from '@/components/TripSummaryCard.vue'
import GroupSummaryCard    from '@/components/GroupSummaryCard.vue'
import UserInfoCard        from '@/components/UserInfoCard.vue'
import InvoiceInfoCard     from '@/components/InvoiceInfoCard.vue'
import LiveTracking        from '@/components/LiveTracking.vue'
import TravelTipCard       from '@/components/TravelTipCard.vue'
import SharePlatformQR     from '@/components/SharePlatformQR.vue'
import ChatbotWidget       from '@/components/ChatbotWidget.vue'

const handleTripChange   = () => {}
const handleGroupChange  = () => {}
const handleInfoChange   = () => {}
const handleInvChange    = () => {}
</script>

<template>
  <main class="p-6 relative">
    <div class="max-w-4xl mx-auto space-y-8">
      <!-- Header -->
      <GroupHeader reservationNumber="30000 666 0265" />

      <!-- Welcome / Hero section -->
      <WelcomeMessage userName="Louis" />

      <!-- NEW: Train line progress below welcome -->
      <TrainLineProgress />

      <!-- Main two-column layout -->
      <div class="grid lg:grid-cols-2 gap-6">
        <!-- Left column: summary & QR -->
        <div class="space-y-6">
          <TripSummaryCard
            from="Gent-Sint-Pieters"
            to="Antwerpen centraal"
            datetime="13/01/25, 12:27"
            train="IC 734"
            :onChange="handleTripChange"
          />
          <GroupSummaryCard
            :childrenCount="20"
            :teensCount="0"
            :adultsCount="3"
            :childrenPrice="20"
            :teensPrice="0"
            :adultsPrice="18"
            :totalPrice="38"
            :onChange="handleGroupChange"
          />
          <UserInfoCard
            name="Margaux Van Linthoudt"
            organization="Chiro Eppegem"
            phone="+32 474 12 34 56"
            email="margaux@mail.com"
            :onChange="handleInfoChange"
          />
          <InvoiceInfoCard
            organization="Chiro Eppegem vzw"
            address="adres 123, 4321 Gemeente"
            :onChange="handleInvChange"
          />

          <!-- QR code widget -->
          <SharePlatformQR link="https://yourapp.com/group/30000-666-0265" />
        </div>

        <!-- Right column: live tracking & tips -->
        <div class="space-y-14">
          <LiveTracking />
          <TravelTipCard
            station="Gent-Sint-Pieters"
            type="departure"
            reservedCoach="5"
            :tips="[
              'Arrive 20 minutes early with your group.',
              'Use the meeting point at the station entrance.'
            ]"
            :warnings="[
              'Move safely as a group through the station. Stay behind the platform line.'
            ]"
            infoLink="/tips"
          />
        </div>
      </div>
    </div>

    <!-- Always-on chatbot widget -->
    <ChatbotWidget />
  </main>
</template>
