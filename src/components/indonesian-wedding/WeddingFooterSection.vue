<template>
  <footer class="wedding-footer-section">
    <div class="container">
      <div class="footer-content">
        <div class="footer-heart">
          <span class="heart">❤️</span>
        </div>
        <h3 class="footer-names">Sarah & Michael</h3>
        <p class="footer-date">December 20, 2025</p>
        <div class="footer-hashtag">#SarahMeetsHerMichael</div>
        <p class="footer-tagline">Thank you for being part of our special day</p>
      </div>
      
      <div class="footer-bottom">
        <p>© {{ currentYear }} Sarah & Michael Wedding | Made with 💜 and Vue.js</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'WeddingFooterSection',
  data() {
    return {
      currentYear: new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.wedding-footer-section {
  background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
  color: white;
  padding: 3rem 0 1.5rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.footer-content {
  text-align: center;
  padding-bottom: 2rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.footer-heart {
  margin-bottom: 1rem;
}

.heart {
  font-size: 3rem;
  display: inline-block;
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

.footer-names {
  font-family: 'Georgia', serif;
  font-size: 2rem;
  color: #f093fb;
  margin-bottom: 0.5rem;
  font-weight: 300;
}

.footer-date {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 1rem;
}

.footer-hashtag {
  display: inline-block;
  font-family: monospace;
  font-size: 1.2rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 1rem;
}

.footer-tagline {
  font-style: italic;
  color: rgba(255, 255, 255, 0.7);
  font-size: 1rem;
}

.footer-bottom {
  text-align: center;
  padding-top: 1.5rem;
}

.footer-bottom p {
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
  margin: 0;
}

@media (max-width: 768px) {
  .wedding-footer-section {
    padding: 2rem 0 1rem;
  }

  .footer-names {
    font-size: 1.5rem;
  }

  .heart {
    font-size: 2rem;
  }

  .footer-hashtag {
    font-size: 1rem;
  }
}
</style>

