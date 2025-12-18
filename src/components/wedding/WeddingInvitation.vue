<template>
  <div class="wedding-invitation">
    <WeddingHero />
    <WeddingDetails />
    <WeddingTimeline />
    <WeddingVenue />
    <WeddingGallery />
    <WeddingRSVP />
    <WeddingFooter />
  </div>
</template>

<script>
import WeddingHero from './WeddingHero.vue'
import WeddingDetails from './WeddingDetails.vue'
import WeddingTimeline from './WeddingTimeline.vue'
import WeddingVenue from './WeddingVenue.vue'
import WeddingGallery from './WeddingGallery.vue'
import WeddingRSVP from './WeddingRSVP.vue'
import WeddingFooter from './WeddingFooter.vue'

export default {
  name: 'WeddingInvitation',
  components: {
    WeddingHero,
    WeddingDetails,
    WeddingTimeline,
    WeddingVenue,
    WeddingGallery,
    WeddingRSVP,
    WeddingFooter
  }
}
</script>

<style scoped>
.wedding-invitation {
  background-color: #fefefe;
}
</style>

