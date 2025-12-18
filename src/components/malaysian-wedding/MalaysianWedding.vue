<template>
  <div class="malaysian-wedding" :class="{ 'invitation-opened': isInvitationOpen }">
    <!-- Cover/Envelope -->
    <transition name="fade">
      <CoverSection 
        v-if="!isInvitationOpen" 
        @open-invitation="openInvitation"
      />
    </transition>

    <!-- Main Invitation Content -->
    <transition name="slide-up">
      <div v-if="isInvitationOpen" class="invitation-content">
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
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    openInvitation() {
      this.isInvitationOpen = true
    },
    handleScroll() {
      this.scrollY = window.scrollY
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
}

.invitation-content {
  animation: fadeIn 1s ease-out;
  position: relative;
  z-index: 1;
  min-height: 100%;
  max-width: 1080px;
  margin: 0 auto;
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

/* Responsive layout tweaks */
@media (min-width: 768px) {
  .invitation-content {
    padding: 2rem 2rem 4rem;
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

