<template>
  <footer class="footer-section" ref="section">
    <div class="container">
      <div class="wedding-date" :class="{ 'fade-in': isVisible }">
        <span class="date-number" style="animation-delay: 0s">15</span>
        <span class="date-dot">•</span>
        <span class="date-number" style="animation-delay: 0.1s">03</span>
        <span class="date-dot">•</span>
        <span class="date-number" style="animation-delay: 0.2s">2026</span>
      </div>

      <div class="closing-quote" :class="{ 'fade-in': isVisible }" style="animation-delay: 0.3s">
        <p>"...and they live happily ever after"</p>
      </div>

      <div class="couple-initials" :class="{ 'scale-in': isVisible }">
        <span class="initial">A</span>
        <span class="heart">❤️</span>
        <span class="initial">R</span>
      </div>

      <div class="social-links" :class="{ 'fade-in': isVisible }" style="animation-delay: 0.5s">
        <a href="#" class="social-link" title="Follow us on Instagram">
          <span class="social-icon">📷</span>
          <span class="social-text">@aisharayyan</span>
        </a>
      </div>

      <div class="crafted-by" :class="{ 'fade-in': isVisible }" style="animation-delay: 0.7s">
        <p>crafted with 💜 using Vue.js</p>
        <p class="credit">Inspired by <a href="https://www.sepasangselamanya.com" target="_blank">sepasang selamanya</a></p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'FooterSection',
  data() {
    return {
      isVisible: false
    }
  },
  mounted() {
    window.addEventListener('scroll', this.checkVisibility)
    this.checkVisibility()
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.checkVisibility)
  },
  methods: {
    checkVisibility() {
      if (this.$refs.section) {
        const rect = this.$refs.section.getBoundingClientRect()
        this.isVisible = rect.top < window.innerHeight * 0.9
      }
    }
  }
}
</script>

<style scoped>
.footer-section {
  padding: 3rem 0 1.5rem;
  background: linear-gradient(to bottom, transparent, rgba(212, 175, 55, 0.08));
  text-align: center;
  overflow: hidden;
}

/* Parallax animations */
.wedding-date,
.closing-quote,
.social-links,
.crafted-by {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s ease-out;
}

.wedding-date.fade-in,
.closing-quote.fade-in,
.social-links.fade-in,
.crafted-by.fade-in {
  opacity: 1;
  transform: translateY(0);
}

.couple-initials {
  opacity: 0;
  transform: scale(0.8);
  transition: all 0.6s ease-out 0.4s;
}

.couple-initials.scale-in {
  opacity: 1;
  transform: scale(1);
}

.date-number {
  animation: fadeInUp 0.5s ease-out both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 2rem;
}

.wedding-date {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 2rem;
}

.date-number {
  font-size: 2rem;
  color: #d4af37;
  font-weight: 300;
}

.date-dot {
  font-size: 1.5rem;
  color: #a0917b;
}

.closing-quote {
  margin-bottom: 2rem;
}

.closing-quote p {
  font-size: 1.2rem;
  color: #5c4a3d;
  font-style: italic;
  font-weight: 300;
}

.couple-initials {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.initial {
  font-size: 2rem;
  color: #d4af37;
  font-weight: 300;
  font-family: 'Georgia', serif;
}

.heart {
  font-size: 1.5rem;
  animation: heartbeat 1.5s ease infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.social-links {
  margin-bottom: 3rem;
}

.social-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(212, 175, 55, 0.3);
  border-radius: 50px;
  color: #5c4a3d;
  text-decoration: none;
  transition: all 0.3s;
}

.social-link:hover {
  background: rgba(255, 255, 255, 1);
  border-color: #d4af37;
  color: #d4af37;
}

.social-icon {
  font-size: 1.2rem;
}

.social-text {
  font-size: 0.95rem;
}

.crafted-by {
  border-top: 1px solid rgba(212, 175, 55, 0.2);
  padding-top: 2rem;
}

.crafted-by p {
  color: #a0917b;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.credit a {
  color: #d4af37;
  text-decoration: none;
}

.credit a:hover {
  text-decoration: underline;
}
</style>

