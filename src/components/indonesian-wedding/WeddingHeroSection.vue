<template>
  <section class="hero-section">
    <div class="hero-background">
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="wedding-badge">WEDDING INVITATION</div>
        <h1 class="couple-names">
          <span class="bride-name">{{ brideName }}</span>
          <span class="ampersand">&</span>
          <span class="groom-name">{{ groomName }}</span>
        </h1>
        <div class="hashtag">#{{ hashtag }}</div>
        <button class="rsvp-button" @click="scrollToRSVP">
          RSVP Now
        </button>
        <div class="scroll-indicator">
          <span>↓</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingHeroSection',
  data() {
    return {
      brideName: 'Sarah',
      groomName: 'Michael',
      hashtag: 'SarahMeetsHerMichael'
    }
  },
  methods: {
    scrollToRSVP() {
      const rsvpSection = document.querySelector('.rsvp-section')
      if (rsvpSection) {
        rsvpSection.scrollIntoView({ behavior: 'smooth' })
      }
    }
  }
}
</script>

<style scoped>
.hero-section {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-background {
  position: relative;
  width: 100%;
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="%23ffffff" fill-opacity="0.05" d="M0,96L48,112C96,128,192,160,288,160C384,160,480,128,576,112C672,96,768,96,864,112C960,128,1056,160,1152,160C1248,160,1344,128,1392,112L1440,96L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path></svg>');
  background-size: cover;
  background-position: bottom;
}

.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 2rem;
  color: white;
}

.wedding-badge {
  display: inline-block;
  padding: 0.5rem 1.5rem;
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid white;
  border-radius: 50px;
  font-size: 0.9rem;
  letter-spacing: 3px;
  margin-bottom: 2rem;
  backdrop-filter: blur(10px);
  animation: fadeInDown 1s ease-out;
}

.couple-names {
  font-family: 'Georgia', serif;
  font-size: clamp(2.5rem, 8vw, 5rem);
  margin-bottom: 1.5rem;
  font-weight: 300;
  line-height: 1.2;
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
  font-size: 2.5rem;
  margin: 1rem 0;
  font-style: italic;
  opacity: 0.9;
}

.hashtag {
  font-size: 1.8rem;
  font-family: monospace;
  margin-bottom: 2rem;
  opacity: 0.95;
  font-weight: 600;
  animation: fadeIn 1s ease-out 0.6s backwards;
}

.rsvp-button {
  padding: 1rem 3rem;
  background: white;
  color: #764ba2;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  animation: fadeIn 1s ease-out 0.9s backwards;
}

.rsvp-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 12px 35px rgba(0, 0, 0, 0.25);
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 2rem;
  animation: bounce 2s infinite;
  opacity: 0.8;
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
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

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

@media (max-width: 768px) {
  .hashtag {
    font-size: 1.3rem;
  }

  .rsvp-button {
    padding: 0.75rem 2rem;
    font-size: 1rem;
  }
}
</style>

