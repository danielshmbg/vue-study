<template>
  <footer class="wedding-footer">
    <div class="container">
      <div class="footer-heart">
        <span class="heart">❤️</span>
      </div>
      <h3 class="footer-names">Emily & James</h3>
      <p class="footer-date">June 15, 2026</p>
      <p class="footer-tagline">Two hearts, one love, forever together</p>
      
      <div class="footer-links">
        <a href="#hero">Home</a>
        <span class="separator">•</span>
        <a href="#details">Details</a>
        <span class="separator">•</span>
        <a href="#timeline">Timeline</a>
        <span class="separator">•</span>
        <a href="#venue">Venue</a>
        <span class="separator">•</span>
        <a href="#gallery">Gallery</a>
        <span class="separator">•</span>
        <a href="#rsvp">RSVP</a>
      </div>

      <div class="footer-social">
        <p class="social-text">Follow our wedding journey</p>
        <div class="social-hashtag">#EmilyAndJames2026</div>
      </div>

      <div class="footer-bottom">
        <p>© {{ currentYear }} Emily & James Wedding</p>
        <p class="footer-note">Made with love and Vue.js 💚</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'WeddingFooter',
  data() {
    return {
      currentYear: new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.wedding-footer {
  background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
  color: white;
  padding: 3rem 0 1.5rem;
  text-align: center;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
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
    transform: scale(1.1);
  }
}

.footer-names {
  font-family: 'Georgia', serif;
  font-size: 2rem;
  color: #d4af37;
  margin-bottom: 0.5rem;
  font-weight: 300;
}

.footer-date {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 0.5rem;
}

.footer-tagline {
  font-style: italic;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 2rem;
  font-size: 1rem;
}

.footer-links {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-bottom: 2rem;
  padding: 1.5rem 0;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.footer-links a {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  transition: color 0.3s;
  font-size: 0.95rem;
  font-weight: 500;
}

.footer-links a:hover {
  color: #d4af37;
}

.separator {
  color: rgba(255, 255, 255, 0.3);
}

.footer-social {
  margin-bottom: 2rem;
}

.social-text {
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 1rem;
}

.social-hashtag {
  display: inline-block;
  background: linear-gradient(135deg, #d4af37, #f0e68c);
  color: #2c3e50;
  padding: 0.5rem 1.5rem;
  border-radius: 50px;
  font-weight: 700;
  font-family: monospace;
  font-size: 1.1rem;
  transition: transform 0.3s;
  cursor: pointer;
}

.social-hashtag:hover {
  transform: scale(1.05);
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 1.5rem;
}

.footer-bottom p {
  color: rgba(255, 255, 255, 0.6);
  margin: 0.25rem 0;
  font-size: 0.9rem;
}

.footer-note {
  font-style: italic;
}

@media (max-width: 768px) {
  .wedding-footer {
    padding: 2rem 0 1rem;
  }

  .footer-names {
    font-size: 1.5rem;
  }

  .footer-links {
    gap: 0.5rem;
    font-size: 0.9rem;
  }

  .heart {
    font-size: 2rem;
  }
}
</style>

