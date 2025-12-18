<template>
  <section class="couple-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">We're Getting Married</h2>
        <p class="section-subtitle">Join us for a fun and happy celebration as we tie the knot!</p>
      </div>

      <div class="couple-grid">
        <div class="person-card">
          <div class="person-photo">
            <div class="photo-placeholder bride-photo">
              <span class="photo-icon">👰</span>
            </div>
          </div>
          <h3 class="person-name">{{ brideName }}</h3>
          <p class="person-details">Daughter of</p>
          <p class="parent-names">{{ brideParents }}</p>
        </div>

        <div class="couple-divider">
          <div class="heart-icon">❤️</div>
        </div>

        <div class="person-card">
          <div class="person-photo">
            <div class="photo-placeholder groom-photo">
              <span class="photo-icon">🤵</span>
            </div>
          </div>
          <h3 class="person-name">{{ groomName }}</h3>
          <p class="person-details">Son of</p>
          <p class="parent-names">{{ groomParents }}</p>
        </div>
      </div>

      <div class="intro-quote">
        <p class="quote-text">
          "{{ quoteText }}"
        </p>
        <p class="quote-source">— {{ quoteSource }}</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'CoupleSection',
  data() {
    return {
      brideName: 'Sarah Anderson',
      brideParents: 'Mr. & Mrs. Robert Anderson',
      groomName: 'Michael Chen',
      groomParents: 'Mr. & Mrs. William Chen',
      quoteText: 'Long before our eyes met, God wrote your name beside mine. In His perfect time, love walks in — not by chance, but by divine design.',
      quoteSource: 'Inspired by Proverbs 19:21'
    }
  }
}
</script>

<style scoped>
.couple-section {
  padding: 5rem 0;
  background: linear-gradient(to bottom, #fdfbf7 0%, #ffffff 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-family: 'Georgia', serif;
  font-size: clamp(2rem, 5vw, 3rem);
  color: #764ba2;
  margin-bottom: 1rem;
  font-weight: 400;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #666;
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.couple-grid {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  gap: 3rem;
  align-items: center;
  margin-bottom: 4rem;
}

.person-card {
  text-align: center;
}

.person-photo {
  margin-bottom: 1.5rem;
}

.photo-placeholder {
  width: 250px;
  height: 250px;
  margin: 0 auto;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  border: 5px solid white;
  position: relative;
  overflow: hidden;
  transition: transform 0.3s;
}

.photo-placeholder:hover {
  transform: scale(1.05);
}

.bride-photo {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
}

.groom-photo {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.photo-icon {
  font-size: 6rem;
  filter: blur(3px);
  opacity: 0.6;
}

.person-name {
  font-family: 'Georgia', serif;
  font-size: 1.8rem;
  color: #2c3e50;
  margin-bottom: 0.5rem;
  font-weight: 400;
}

.person-details {
  color: #888;
  font-size: 0.95rem;
  margin-bottom: 0.25rem;
}

.parent-names {
  color: #555;
  font-weight: 600;
  font-size: 1.05rem;
}

.couple-divider {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.heart-icon {
  font-size: 3rem;
  animation: heartbeat 1.5s ease infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.15);
  }
}

.intro-quote {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 3rem;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 40px rgba(118, 75, 162, 0.2);
  max-width: 800px;
  margin: 0 auto;
}

.quote-text {
  font-size: 1.2rem;
  color: white;
  line-height: 1.8;
  font-style: italic;
  margin-bottom: 1rem;
}

.quote-source {
  color: rgba(255, 255, 255, 0.8);
  font-size: 0.95rem;
  font-weight: 600;
}

@media (max-width: 968px) {
  .couple-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .couple-divider {
    order: 2;
    transform: rotate(90deg);
  }

  .person-card:first-child {
    order: 1;
  }

  .person-card:last-child {
    order: 3;
  }

  .photo-placeholder {
    width: 200px;
    height: 200px;
  }

  .photo-icon {
    font-size: 5rem;
  }
}

@media (max-width: 768px) {
  .couple-section {
    padding: 3rem 0;
  }

  .intro-quote {
    padding: 2rem;
  }

  .quote-text {
    font-size: 1rem;
  }
}
</style>

