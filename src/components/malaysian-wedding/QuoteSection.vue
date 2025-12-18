<template>
  <section class="quote-section" ref="section">
    <div class="container">
      <div 
        class="quote-decoration"
        :style="{ transform: `translateY(${parallaxOffset * 0.1}px)` }"
      >
        <span 
          class="deco-left"
          :style="{ transform: `rotate(${parallaxOffset * 0.02}deg)` }"
        >❦</span>
        <span 
          class="deco-right"
          :style="{ transform: `scaleX(-1) rotate(${parallaxOffset * -0.02}deg)` }"
        >❦</span>
      </div>
      
      <div 
        class="quote-content"
        :class="{ 'fade-in-visible': isVisible }"
      >
        <div 
          class="quote-mark open"
          :style="{ transform: `translateX(${parallaxOffset * -0.05}px)` }"
        >"</div>
        <p class="quote-text">{{ quoteText }}</p>
        <div 
          class="quote-mark close"
          :style="{ transform: `translateX(${parallaxOffset * 0.05}px)` }"
        >"</div>
        <p class="quote-source">{{ quoteSource }}</p>
      </div>

      <div 
        class="divider"
        :style="{ transform: `scaleX(${1 + parallaxOffset * 0.0005})` }"
      >
        <span class="divider-line"></span>
        <span 
          class="divider-ornament"
          :style="{ transform: `rotate(${parallaxOffset * 0.1}deg)` }"
        >✦</span>
        <span class="divider-line"></span>
      </div>

      <p 
        class="invitation-text"
        :style="{ transform: `translateY(${parallaxOffset * -0.05}px)` }"
      >
        We cordially invite you to celebrate our wedding
      </p>
    </div>
  </section>
</template>

<script>
export default {
  name: 'QuoteSection',
  props: {
    scrollY: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      quoteText: 'And one of His signs is that He created for you spouses from among yourselves so that you may find comfort in them. And He has placed between you compassion and mercy. Surely in this are signs for people who reflect.',
      quoteSource: '(Q.S. Ar-Rum: 21)',
      sectionTop: 0,
      isVisible: false
    }
  },
  computed: {
    parallaxOffset() {
      return Math.max(0, this.scrollY - this.sectionTop + 400)
    }
  },
  mounted() {
    this.updateSectionTop()
    window.addEventListener('resize', this.updateSectionTop)
    this.checkVisibility()
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.updateSectionTop)
  },
  watch: {
    scrollY() {
      this.checkVisibility()
    }
  },
  methods: {
    updateSectionTop() {
      if (this.$refs.section) {
        this.sectionTop = this.$refs.section.offsetTop
      }
    },
    checkVisibility() {
      if (this.$refs.section) {
        const rect = this.$refs.section.getBoundingClientRect()
        this.isVisible = rect.top < window.innerHeight * 0.8
      }
    }
  }
}
</script>

<style scoped>
.quote-section {
  padding: 3rem 0;
  /* background: linear-gradient(to bottom, transparent, rgba(212, 175, 55, 0.05), transparent); */
  position: relative;
  overflow: hidden;
  background-image: url('https://cloudinary-a.akamaihd.net/drdikhiur/image/upload/v1713430701/contents/Ima-Gatot/Watercolor/vectors/loading-bg_yuz8kz.webp');
  background-repeat:no-repeat;
  background-size:cover;
  background-position:center;
}

/* Fade-in animation on scroll */
.quote-content {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.quote-content.fade-in-visible {
  opacity: 1;
  transform: translateY(0);
}

.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 2rem;
  text-align: center;
}

.quote-decoration {
  position: relative;
  margin-bottom: 2rem;
}

.deco-left,
.deco-right {
  font-size: 2rem;
  color: #d4af37;
  opacity: 0.5;
}

.deco-left {
  margin-right: 2rem;
}

.deco-right {
  margin-left: 2rem;
  transform: scaleX(-1);
  display: inline-block;
}

.quote-content {
  position: relative;
  padding: 2rem 0;
}

.quote-mark {
  font-size: 4rem;
  color: #d4af37;
  opacity: 0.3;
  font-family: Georgia, serif;
  line-height: 1;
  position: absolute;
}

.quote-mark.open {
  top: 0;
  left: 0;
}

.quote-mark.close {
  bottom: 0;
  right: 0;
}

.quote-text {
  font-size: 1rem;
  line-height: 2;
  color: #5c4a3d;
  font-style: italic;
  padding: 0 1rem;
  margin-bottom: 1.5rem;
}

.quote-source {
  font-size: 1rem;
  color: #d4af37;
  font-weight: 600;
  letter-spacing: 1px;
}

.divider {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin: 3rem 0;
}

.divider-line {
  width: 60px;
  height: 1px;
  background: linear-gradient(to right, transparent, rgba(212, 175, 55, 0.5), transparent);
}

.divider-ornament {
  color: #d4af37;
  font-size: 1rem;
}

.invitation-text {
  font-size: 1.2rem;
  color: #5c4a3d;
  font-weight: 300;
  letter-spacing: 2px;
}
</style>

