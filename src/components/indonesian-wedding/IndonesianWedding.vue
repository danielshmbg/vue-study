<template>
  <div class="indonesian-wedding">
    <WeddingHeroSection />
    <CoupleSection />
    <LoveStorySection />
    <EventDetailsSection />
    <RSVPSection />
    <GiftSection />
    <WishesSection />
    <WeddingFooterSection />
  </div>
</template>

<script>
import WeddingHeroSection from './WeddingHeroSection.vue'
import CoupleSection from './CoupleSection.vue'
import LoveStorySection from './LoveStorySection.vue'
import EventDetailsSection from './EventDetailsSection.vue'
import RSVPSection from './RSVPSection.vue'
import GiftSection from './GiftSection.vue'
import WishesSection from './WishesSection.vue'
import WeddingFooterSection from './WeddingFooterSection.vue'

export default {
  name: 'IndonesianWedding',
  components: {
    WeddingHeroSection,
    CoupleSection,
    LoveStorySection,
    EventDetailsSection,
    RSVPSection,
    GiftSection,
    WishesSection,
    WeddingFooterSection
  }
}
</script>

<style scoped>
.indonesian-wedding {
  background-color: #fdfbf7;
  overflow-x: hidden;
}
</style>

