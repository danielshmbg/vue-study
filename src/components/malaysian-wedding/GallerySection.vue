<template>
  <section class="gallery-section" ref="section">
    <div class="container">
      <!-- Header -->
      <div 
        class="section-header"
        :class="{ 'fade-in-visible': isVisible }"
      >
        <h2 class="section-title">Our Moment</h2>
        <p class="section-quote">
          "I was created in time to fill your time, and I use all the time in<br>
          my live to love you."
        </p>
      </div>

      <!-- Horizontal Scrolling Gallery -->
      <div class="gallery-scroll-container">
        <div class="gallery-scroll">
          <div 
            v-for="(photo, index) in photos" 
            :key="index" 
            class="gallery-item"
            @click="openLightbox(index)"
          >
            <img :src="photo.url" :alt="photo.caption" class="gallery-image">
          </div>
        </div>
      </div>

      <!-- Video Section -->
      <div class="video-container">
        <video 
          ref="videoPlayer"
          class="video-player"
          :src="videoUrl"
          @click="toggleVideo"
        ></video>
        <div class="video-controls">
          <button @click="toggleVideo" class="play-pause-btn">
            {{ isPlaying ? '⏸' : '▶' }}
          </button>
          <button @click="toggleMute" class="mute-btn">
            {{ isMuted ? '🔇' : '🔊' }}
          </button>
          <input 
            type="range" 
            class="progress-bar"
            :value="progress"
            @input="seekVideo"
            min="0"
            max="100"
          >
          <span class="time-display">-{{ formatTime(timeRemaining) }}</span>
          <button @click="toggleFullscreen" class="fullscreen-btn">⛶</button>
        </div>
      </div>

      <!-- Lightbox -->
      <transition name="fade">
        <div v-if="lightboxOpen" class="lightbox" @click.self="closeLightbox">
          <button class="lightbox-close" @click="closeLightbox">✕</button>
          <button class="lightbox-nav prev" @click="prevPhoto">❮</button>
          
          <div class="lightbox-content">
            <img :src="photos[currentPhoto].url" :alt="photos[currentPhoto].caption" class="lightbox-image">
            <p class="lightbox-counter">{{ currentPhoto + 1 }} / {{ photos.length }}</p>
          </div>
          
          <button class="lightbox-nav next" @click="nextPhoto">❯</button>
        </div>
      </transition>
    </div>
  </section>
</template>

<script>
export default {
  name: 'GallerySection',
  data() {
    return {
      lightboxOpen: false,
      currentPhoto: 0,
      isVisible: false,
      isPlaying: false,
      isMuted: true,
      progress: 0,
      timeRemaining: 0,
      videoUrl: 'https://res.cloudinary.com/dfht26lv6/video/upload/v1765847361/sample_video_wedding_iuzkrq.mp4',
      photos: [
        { url: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906786/%EF%B8%8F_utuoqs.jpg', caption: 'Photo 1' },
        { url: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906787/ab1f2ffbd2ae575bc19c30177410a4e5_vaj56f.jpg', caption: 'Photo 2' },
        { url: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906787/Alina_Bohdan__two_souls_one_love_endless_summer_light_%EF%B8%8F_bepuen.jpg', caption: 'Photo 3' },
        { url: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906787/7bfec287c9a090e8dc17fef5a1618258_nw1ltl.jpg', caption: 'Photo 4' },
        { url: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906787/7bfec287c9a090e8dc17fef5a1618258_nw1ltl.jpg', caption: 'Photo 5' },
        { url: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906788/be46e99ddb4879835cbf81bd2465bbaa_ya4zsl.jpg', caption: 'Photo 6' }
      ]
    }
  },
  mounted() {
    window.addEventListener('scroll', this.checkVisibility)
    this.checkVisibility()
    
    if (this.$refs.videoPlayer) {
      this.$refs.videoPlayer.addEventListener('timeupdate', this.updateProgress)
      this.$refs.videoPlayer.addEventListener('ended', () => {
        this.isPlaying = false
      })
    }
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.checkVisibility)
    if (this.$refs.videoPlayer) {
      this.$refs.videoPlayer.removeEventListener('timeupdate', this.updateProgress)
    }
  },
  methods: {
    checkVisibility() {
      if (this.$refs.section) {
        const rect = this.$refs.section.getBoundingClientRect()
        this.isVisible = rect.top < window.innerHeight * 0.8
      }
    },
    toggleVideo() {
      const video = this.$refs.videoPlayer
      if (video.paused) {
        video.play()
        this.isPlaying = true
      } else {
        video.pause()
        this.isPlaying = false
      }
    },
    toggleMute() {
      const video = this.$refs.videoPlayer
      video.muted = !video.muted
      this.isMuted = video.muted
    },
    updateProgress() {
      const video = this.$refs.videoPlayer
      if (video.duration) {
        this.progress = (video.currentTime / video.duration) * 100
        this.timeRemaining = video.duration - video.currentTime
      }
    },
    seekVideo(event) {
      const video = this.$refs.videoPlayer
      const seekTime = (event.target.value / 100) * video.duration
      video.currentTime = seekTime
    },
    formatTime(seconds) {
      const mins = Math.floor(seconds / 60)
      const secs = Math.floor(seconds % 60)
      return `${mins}:${secs.toString().padStart(2, '0')}`
    },
    toggleFullscreen() {
      const video = this.$refs.videoPlayer
      if (video.requestFullscreen) {
        video.requestFullscreen()
      } else if (video.webkitRequestFullscreen) {
        video.webkitRequestFullscreen()
      }
    },
    openLightbox(index) {
      this.currentPhoto = index
      this.lightboxOpen = true
      document.body.style.overflow = 'hidden'
    },
    closeLightbox() {
      this.lightboxOpen = false
      document.body.style.overflow = ''
    },
    nextPhoto() {
      this.currentPhoto = (this.currentPhoto + 1) % this.photos.length
    },
    prevPhoto() {
      this.currentPhoto = (this.currentPhoto - 1 + this.photos.length) % this.photos.length
    }
  }
}
</script>

<style scoped>
.gallery-section {
  padding: 4rem 1rem;
  background-color: #fbf3f0;
  overflow: hidden;
}

.container {
  max-width: 900px;
  margin: 0 auto;
}

/* Header */
.section-header {
  text-align: center;
  margin-bottom: 3rem;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.section-header.fade-in-visible {
  opacity: 1;
  transform: translateY(0);
}

.section-title {
  font-size: 5rem;
  font-family: 'Beloved Lovely', cursive;
  color: #2c2c2c;
  font-weight: 300;
  margin-bottom: 1.5rem;
  line-height: 1;
}

.section-quote {
  font-size: 1.1rem;
  color: #2c2c2c;
  line-height: 1.8;
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
  max-width: 600px;
  margin: 0 auto;
}

/* Horizontal Scrolling Gallery */
.gallery-scroll-container {
  margin: 3rem 0;
  overflow: hidden;
}

.gallery-scroll {
  display: flex;
  gap: 1.5rem;
  overflow-x: auto;
  padding: 1rem 0;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}

.gallery-scroll::-webkit-scrollbar {
  height: 8px;
}

.gallery-scroll::-webkit-scrollbar-track {
  background: rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.gallery-scroll::-webkit-scrollbar-thumb {
  background: #6b8e6b;
  border-radius: 10px;
}

.gallery-scroll::-webkit-scrollbar-thumb:hover {
  background: #5a7a5a;
}

.gallery-item {
  flex: 0 0 auto;
  width: 480px;
  height: 600px;
  cursor: pointer;
  transition: transform 0.3s;
  border-radius: 10px;
  overflow: hidden;
}

.gallery-item:hover {
  transform: scale(1.05);
}

.gallery-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* Video Section */
.video-container {
  margin-top: 3rem;
  position: relative;
  background: #000;
  border-radius: 10px;
  overflow: hidden;
}

.video-player {
  width: 100%;
  height: auto;
  display: block;
  cursor: pointer;
}

.video-controls {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  background: #000;
  color: white;
}

.play-pause-btn,
.mute-btn,
.fullscreen-btn {
  background: none;
  border: none;
  color: white;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 0.5rem;
  transition: opacity 0.3s;
}

.play-pause-btn:hover,
.mute-btn:hover,
.fullscreen-btn:hover {
  opacity: 0.7;
}

.progress-bar {
  flex: 1;
  height: 4px;
  -webkit-appearance: none;
  appearance: none;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 2px;
  cursor: pointer;
}

.progress-bar::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 12px;
  height: 12px;
  background: white;
  border-radius: 50%;
  cursor: pointer;
}

.progress-bar::-moz-range-thumb {
  width: 12px;
  height: 12px;
  background: white;
  border-radius: 50%;
  cursor: pointer;
  border: none;
}

.time-display {
  font-size: 0.9rem;
  min-width: 50px;
}

/* Lightbox */
.lightbox {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10000;
}

.lightbox-close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  background: none;
  border: none;
  color: white;
  font-size: 2rem;
  cursor: pointer;
  transition: all 0.3s;
}

.lightbox-close:hover {
  transform: scale(1.2);
  color: #d4af37;
}

.lightbox-nav {
  background: rgba(255, 255, 255, 0.1);
  border: none;
  color: white;
  font-size: 2rem;
  padding: 1rem;
  cursor: pointer;
  transition: all 0.3s;
  border-radius: 50%;
}

.lightbox-nav:hover {
  background: rgba(212, 175, 55, 0.3);
}

.lightbox-nav.prev {
  margin-right: 2rem;
}

.lightbox-nav.next {
  margin-left: 2rem;
}

.lightbox-content {
  text-align: center;
  max-width: 90vw;
  max-height: 90vh;
}

.lightbox-image {
  max-width: 100%;
  max-height: 80vh;
  object-fit: contain;
  border-radius: 10px;
  margin-bottom: 1rem;
}

.lightbox-counter {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1rem;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 3.5rem;
  }

  .section-quote {
    font-size: 1rem;
  }

  .gallery-item {
    width: 220px;
    height: 320px;
  }

  .lightbox-nav {
    font-size: 1.5rem;
    padding: 0.5rem;
  }
}
</style>

