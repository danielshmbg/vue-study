<template>
  <section class="gift-section" ref="section">
    <div class="container">
      <div 
        class="flower-decoration"
        :style="{ transform: `translateY(${parallaxOffset * -0.1}px) rotate(${parallaxOffset * 0.05}deg)` }"
      >🌸</div>
      
      <div 
        class="section-header"
        :class="{ 'fade-in-visible': isVisible }"
      >
        <h2 class="section-title">Wedding Gift</h2>
        <p class="section-subtitle">
          Your love is the greatest gift. Any contributions are graciously accepted.
        </p>
      </div>

      <div class="gift-cards">
        <div 
          v-for="(account, index) in bankAccounts" 
          :key="index" 
          class="gift-card"
          :class="{ 'card-visible': isVisible }"
          :style="{ 
            transitionDelay: `${index * 0.15}s`,
            transform: `translateY(${parallaxOffset * (index % 2 === 0 ? -0.02 : 0.02)}px)`
          }"
        >
          <div 
            class="bank-logo"
            :style="{ transform: `scale(${1 + parallaxOffset * 0.0002})` }"
          >{{ account.icon }}</div>
          <div class="bank-name">{{ account.bank }}</div>
          <div class="account-details">
            <p class="account-number">{{ account.number }}</p>
            <p class="account-name">{{ account.name }}</p>
          </div>
          <button 
            class="copy-btn" 
            @click="copyToClipboard(account.number, index)"
          >
            <span v-if="copiedIndex === index">✓ Copied!</span>
            <span v-else>Copy</span>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'GiftSection',
  props: {
    scrollY: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      copiedIndex: null,
      sectionTop: 0,
      isVisible: false,
      bankAccounts: [
        {
          bank: 'MAYBANK',
          icon: '🏦',
          number: '1234567890',
          name: 'Muhammad Rayyan Bin Ahmad'
        },
        {
          bank: 'MAYBANK',
          icon: '🏦',
          number: '0987654321',
          name: 'Aisha Nur Aisyah Binti Rahman'
        }
      ]
    }
  },
  computed: {
    parallaxOffset() {
      return Math.max(0, this.scrollY - this.sectionTop + 600)
    }
  },
  mounted() {
    this.updateSectionTop()
    window.addEventListener('resize', this.updateSectionTop)
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
    },
    async copyToClipboard(text, index) {
      try {
        await navigator.clipboard.writeText(text)
        this.copiedIndex = index
        setTimeout(() => {
          this.copiedIndex = null
        }, 2000)
      } catch (err) {
        alert(`Account Number: ${text}`)
      }
    }
  }
}
</script>

<style scoped>
.gift-section {
  padding: 3rem 0;
  position: relative;
  overflow: hidden;
}

/* Parallax animations */
.section-header {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.section-header.fade-in-visible {
  opacity: 1;
  transform: translateY(0);
}

.gift-card {
  opacity: 0;
  transform: translateY(40px) scale(0.95);
  transition: all 0.6s ease-out;
}

.gift-card.card-visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
}

.flower-decoration {
  position: absolute;
  top: -1rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 3rem;
  opacity: 0.5;
  animation: sway 3s ease-in-out infinite;
}

@keyframes sway {
  0%, 100% {
    transform: translateX(-50%) rotate(-5deg);
  }
  50% {
    transform: translateX(-50%) rotate(5deg);
  }
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-title {
  font-size: 1.5rem;
  color: #5c4a3d;
  font-weight: 300;
  margin-bottom: 1rem;
}

.section-subtitle {
  font-size: 1.1rem;
  color: #8b7355;
  line-height: 1.6;
  font-style: italic;
}

.gift-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.gift-card {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(212, 175, 55, 0.3);
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  backdrop-filter: blur(10px);
  transition: all 0.3s;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.05);
}

.gift-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
  border-color: #d4af37;
}

.bank-logo {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.bank-name {
  font-size: 1.2rem;
  color: #d4af37;
  font-weight: 700;
  letter-spacing: 3px;
  margin-bottom: 1.5rem;
}

.account-details {
  margin-bottom: 1.5rem;
}

.account-number {
  font-size: 1.3rem;
  color: #5c4a3d;
  font-family: monospace;
  letter-spacing: 2px;
  margin-bottom: 0.5rem;
}

.account-name {
  font-size: 0.95rem;
  color: #8b7355;
  font-weight: 600;
}

.copy-btn {
  padding: 0.75rem 2rem;
  background: linear-gradient(135deg, #d4af37, #f0d78c);
  color: #1a1a2e;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 700;
  font-family: inherit;
  cursor: pointer;
  transition: all 0.3s;
  min-width: 120px;
}

.copy-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 20px rgba(212, 175, 55, 0.3);
}

@media (max-width: 768px) {
  .gift-section {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 1.5rem;
  }

  .gift-cards {
    grid-template-columns: 1fr;
  }

  .gift-card {
    padding: 1.5rem;
  }
}
</style>

