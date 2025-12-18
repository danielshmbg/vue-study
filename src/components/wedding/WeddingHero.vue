<template>
  <section class="wedding-hero">
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <div class="save-the-date">Save the Date</div>
      <h1 class="couple-names">
        <span class="bride-name">{{ brideName }}</span>
        <span class="ampersand">&</span>
        <span class="groom-name">{{ groomName }}</span>
      </h1>
      <div class="wedding-date">{{ weddingDate }}</div>
      <div class="countdown">
        <div class="countdown-item">
          <div class="countdown-number">{{ countdown.days }}</div>
          <div class="countdown-label">Days</div>
        </div>
        <div class="countdown-item">
          <div class="countdown-number">{{ countdown.hours }}</div>
          <div class="countdown-label">Hours</div>
        </div>
        <div class="countdown-item">
          <div class="countdown-number">{{ countdown.minutes }}</div>
          <div class="countdown-label">Minutes</div>
        </div>
        <div class="countdown-item">
          <div class="countdown-number">{{ countdown.seconds }}</div>
          <div class="countdown-label">Seconds</div>
        </div>
      </div>
      <button class="scroll-down" @click="scrollToDetails">
        <span>↓</span>
      </button>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingHero',
  data() {
    return {
      brideName: 'Emily',
      groomName: 'James',
      weddingDate: 'June 15, 2026',
      weddingDateTime: new Date('2026-06-15T16:00:00'),
      countdown: {
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0
      },
      countdownInterval: null
    }
  },
  mounted() {
    this.updateCountdown()
    this.countdownInterval = setInterval(this.updateCountdown, 1000)
  },
  beforeUnmount() {
    if (this.countdownInterval) {
      clearInterval(this.countdownInterval)
    }
  },
  methods: {
    updateCountdown() {
      const now = new Date().getTime()
      const distance = this.weddingDateTime.getTime() - now

      if (distance > 0) {
        this.countdown.days = Math.floor(distance / (1000 * 60 * 60 * 24))
        this.countdown.hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
        this.countdown.minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60))
        this.countdown.seconds = Math.floor((distance % (1000 * 60)) / 1000)
      }
    },
    scrollToDetails() {
      window.scrollTo({
        top: window.innerHeight,
        behavior: 'smooth'
      })
    }
  }
}
</script>

<style scoped>
.wedding-hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  background-image: 
    linear-gradient(135deg, rgba(245, 247, 250, 0.95) 0%, rgba(195, 207, 226, 0.95) 100%),
    url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="%23ffffff" fill-opacity="0.1" d="M0,96L48,112C96,128,192,160,288,160C384,160,480,128,576,112C672,96,768,96,864,112C960,128,1056,160,1152,160C1248,160,1344,128,1392,112L1440,96L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path></svg>');
  background-size: cover;
  background-position: center;
  text-align: center;
  overflow: hidden;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at center, transparent 0%, rgba(255, 255, 255, 0.3) 100%);
}

.hero-content {
  position: relative;
  z-index: 1;
  padding: 2rem;
  max-width: 800px;
}

.save-the-date {
  font-size: 1.2rem;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #8b7355;
  margin-bottom: 2rem;
  font-weight: 300;
}

.couple-names {
  font-family: 'Georgia', serif;
  font-size: clamp(2.5rem, 8vw, 5rem);
  color: #2c3e50;
  margin-bottom: 1.5rem;
  line-height: 1.2;
  font-weight: 300;
}

.bride-name,
.groom-name {
  display: block;
  animation: fadeInUp 1s ease-out;
}

.groom-name {
  animation-delay: 0.3s;
  opacity: 0;
  animation-fill-mode: forwards;
}

.ampersand {
  display: block;
  font-size: 3rem;
  color: #d4af37;
  margin: 1rem 0;
  font-style: italic;
}

.wedding-date {
  font-size: 1.5rem;
  color: #555;
  margin-bottom: 3rem;
  letter-spacing: 1px;
}

.countdown {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin: 3rem 0;
  flex-wrap: wrap;
}

.countdown-item {
  text-align: center;
}

.countdown-number {
  font-size: 3rem;
  font-weight: 700;
  color: #d4af37;
  line-height: 1;
}

.countdown-label {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: #8b7355;
  margin-top: 0.5rem;
}

.scroll-down {
  background: none;
  border: 2px solid #d4af37;
  color: #d4af37;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  font-size: 1.5rem;
  cursor: pointer;
  margin-top: 2rem;
  animation: bounce 2s infinite;
  transition: all 0.3s;
}

.scroll-down:hover {
  background-color: #d4af37;
  color: white;
  transform: scale(1.1);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

@media (max-width: 768px) {
  .countdown {
    gap: 1rem;
  }

  .countdown-number {
    font-size: 2rem;
  }

  .countdown-label {
    font-size: 0.75rem;
  }

  .ampersand {
    font-size: 2rem;
    margin: 0.5rem 0;
  }
}
</style>

