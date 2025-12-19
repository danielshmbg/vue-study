<template>
  <div class="malaysian-wedding" :class="{ 'invitation-opened': isInvitationOpen }">
    
    <section class="invitation-content-section">
      <!-- Cover/Envelope -->
    <CoverSection class="cover-section" />
    <!-- Main Invitation Content -->
    <div class="invitation-content-container">
      <transition name="slide-up">
      <div class="invitation-content">
        <AudioPlayer />
        <HeroSection :scroll-y="scrollY" />
        <CoupleSection :scroll-y="scrollY" />
        <GallerySection />
        <LoveStorySection />
        <RSVPSection :scroll-y="scrollY" />
        <GiftSection :scroll-y="scrollY" />
        <FooterSection />
      </div>
    </transition>
    </div>
     </section>
    
    
    <!-- Parallax Stars Background -->
    <div class="parallax-stars" :style="{ transform: `translateY(${scrollY * 0.3}px)` }">
      <div class="star" v-for="n in 50" :key="n" :style="getStarStyle(n)"></div>
    </div>
  </div>
</template>

<script>
import CoverSection from './CoverSection.vue'
import AudioPlayer from './AudioPlayer.vue'
import HeroSection from './HeroSection.vue'
import CoupleSection from './CoupleSection.vue'
import GallerySection from './GallerySection.vue'
import LoveStorySection from './LoveStorySection.vue'
import RSVPSection from './RSVPSection.vue'
import GiftSection from './GiftSection.vue'
import FooterSection from './FooterSection.vue'

export default {
  name: 'MalaysianWedding',
  components: {
    CoverSection,
    AudioPlayer,
    HeroSection,
    CoupleSection,
    GallerySection,
    LoveStorySection,
    RSVPSection,
    GiftSection,
    FooterSection
  },
  data() {
    return {
      isInvitationOpen: false,
      scrollY: 0
    }
  },
  mounted() {
    // Listen to scroll on the invitation-content-container instead of window
    this.$nextTick(() => {
      const scrollContainer = this.$el.querySelector('.invitation-content-container')
      if (scrollContainer) {
        scrollContainer.addEventListener('scroll', this.handleScroll)
      }
    })
  },
  beforeUnmount() {
    const scrollContainer = this.$el.querySelector('.invitation-content-container')
    if (scrollContainer) {
      scrollContainer.removeEventListener('scroll', this.handleScroll)
    }
  },
  methods: {
    openInvitation() {
      this.isInvitationOpen = true
    },
    handleScroll(event) {
      this.scrollY = event.target.scrollTop
    },
    getStarStyle(n) {
      const seed = n * 137.5
      return {
        left: `${(seed % 100)}%`,
        top: `${((seed * 2.3) % 100)}%`,
        width: `${(n % 3) + 1}px`,
        height: `${(n % 3) + 1}px`,
        animationDelay: `${(n % 5) * 0.5}s`
      }
    }
  }
}
</script>

<style scoped>
.malaysian-wedding {
  min-height: 100vh;
  background: linear-gradient(135deg, #fdfcfb 0%, #f5f0e8 50%, #ebe4d8 100%);
  color: #4a4a4a;
  font-family: 'Georgia', serif;
  overflow-x: hidden;
  position: relative;
  background-image: url('https://res.cloudinary.com/dfht26lv6/image/upload/v1765707470/hero_page_desktop_vmaklm.png');
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  display: block;
}

.invitation-content {
  animation: fadeIn 1s ease-out;
  position: relative;
  z-index: 1;
  min-height: 100%;
  margin: 0 auto;
}

.invitation-content-section{
  display: flex;
  flex-direction: row;
  min-height: 100vh;
  gap: 0;
}

.invitation-content-container{
  width: 39%;
  flex-shrink: 0;
  overflow-y: auto;
  height: 100vh;
  position: sticky;
  top: 0;
}

.cover-section {
  width: 61%;
  flex-shrink: 0;
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
}

/* Parallax Petals Background */
.parallax-stars {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 200%;
  pointer-events: none;
  z-index: 0;
}

.star {
  position: absolute;
  background: linear-gradient(135deg, #d4af37, #f0d78c);
  border-radius: 50%;
  opacity: 0.3;
  animation: twinkle 3s ease-in-out infinite;
}

@keyframes twinkle {
  0%, 100% {
    opacity: 0.15;
    transform: scale(1);
  }
  50% {
    opacity: 0.4;
    transform: scale(1.2);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}


/* Mobile Responsive */
@media (max-width: 768px) {
  .invitation-content-section {
    flex-direction: column;
  }
  
  .cover-section {
    display: none;
  }
  
  .invitation-content-container {
    width: 100%;
    height: 100vh;
  }
  
  .invitation-content {
    max-width: 100%;
    padding: 0;
  }
}

@media (min-width: 1200px) {
  .invitation-content {
    padding-left: 0;
    padding-right: 0;
  }
}

.slide-up-enter-active {
  transition: all 0.8s ease-out;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>

