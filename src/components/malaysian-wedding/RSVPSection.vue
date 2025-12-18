<template>
  <section class="rsvp-section" ref="section">
    <div class="container">
      <div 
        class="section-header"
        :class="{ 'fade-in-visible': isVisible }"
        :style="{ transform: `translateY(${parallaxOffset * -0.05}px)` }"
      >
        <div class="names-display">
          <span 
            class="name"
            :style="{ transform: `translateX(${parallaxOffset * -0.03}px)` }"
          >Aisha</span>
          <span class="ampersand">&</span>
          <span 
            class="name"
            :style="{ transform: `translateX(${parallaxOffset * 0.03}px)` }"
          >Rayyan</span>
        </div>
        <h2 class="section-title">RSVP</h2>
      </div>

      <div 
        class="rsvp-card"
        :class="{ 'slide-up-visible': isVisible }"
      >
        <form @submit.prevent="handleSubmit" class="rsvp-form">
          <div class="form-group">
            <label for="name">Name</label>
            <input 
              type="text" 
              id="name" 
              v-model="formData.name" 
              placeholder="Your full name"
              required
            >
          </div>

          <div class="form-group">
            <label for="wishes">Wishes</label>
            <textarea 
              id="wishes" 
              v-model="formData.wishes" 
              rows="4"
              placeholder="Write your wishes for the couple..."
            ></textarea>
          </div>

          <div class="form-group">
            <label>Attendance</label>
            <div class="attendance-options">
              <label class="attendance-option">
                <input 
                  type="radio" 
                  value="yes" 
                  v-model="formData.attending"
                  required
                >
                <span class="option-box attend">
                  <span class="option-icon">✓</span>
                  <span class="option-text">I will attend</span>
                </span>
              </label>
              <label class="attendance-option">
                <input 
                  type="radio" 
                  value="no" 
                  v-model="formData.attending"
                  required
                >
                <span class="option-box decline">
                  <span class="option-icon">✗</span>
                  <span class="option-text">Sorry, I won't be able to attend</span>
                </span>
              </label>
            </div>
          </div>

          <button type="submit" class="submit-btn" :disabled="isSubmitting">
            <span v-if="!isSubmitting">Submit</span>
            <span v-else>Sending...</span>
          </button>

          <p v-if="submitMessage" class="submit-message" :class="{ success: isSuccess }">
            {{ submitMessage }}
          </p>
        </form>
      </div>

      <!-- Wishes Display -->
      <div class="wishes-section">
        <h3 class="wishes-title">Wishes</h3>
        <div class="scroll-hint">
          <span class="scroll-icon">↕️</span>
        </div>
        
        <div class="wishes-list">
          <div 
            v-for="(wish, index) in wishes" 
            :key="index" 
            class="wish-card"
          >
            <div class="wish-avatar">{{ getInitials(wish.name) }}</div>
            <div class="wish-content">
              <h4 class="wish-name">{{ wish.name }}</h4>
              <p class="wish-text">{{ wish.message }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'RSVPSection',
  props: {
    scrollY: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      formData: {
        name: '',
        wishes: '',
        attending: ''
      },
      isSubmitting: false,
      submitMessage: '',
      isSuccess: false,
      wishes: [
        { name: 'Fatimah Ahmad', message: 'Congratulations on your wedding! Wishing you both a lifetime of happiness and love. May Allah bless your union! 🎉' },
        { name: 'Muhammad Ali', message: 'So happy for both of you! May your marriage be filled with joy, love, and endless blessings. Congratulations!' },
        { name: 'Nur Aisyah', message: 'Best wishes on this beautiful journey together! May Allah shower His blessings upon you both. ❤️' },
        { name: 'Hassan Ibrahim', message: 'Wishing you both a wonderful life together. Congratulations on your wedding day!' }
      ],
      sectionTop: 0,
      isVisible: false
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
    getInitials(name) {
      return name
        .split(' ')
        .map(word => word[0])
        .join('')
        .toUpperCase()
        .substring(0, 2)
    },
    async handleSubmit() {
      this.isSubmitting = true
      this.submitMessage = ''

      await new Promise(resolve => setTimeout(resolve, 1500))

      if (this.formData.wishes) {
        this.wishes.unshift({
          name: this.formData.name,
          message: this.formData.wishes
        })
      }

      this.isSubmitting = false
      this.isSuccess = true
      this.submitMessage = 'Thank you for your RSVP! 💕'

      setTimeout(() => {
        this.formData = { name: '', wishes: '', attending: '' }
        this.submitMessage = ''
      }, 3000)
    }
  }
}
</script>

<style scoped>
.rsvp-section {
  padding: 3rem 0;
  background: linear-gradient(to bottom, transparent, rgba(212, 175, 55, 0.03));
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

.rsvp-card {
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease-out 0.2s;
}

.rsvp-card.slide-up-visible {
  opacity: 1;
  transform: translateY(0);
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.names-display {
  margin-bottom: 1rem;
}

.names-display .name {
  font-size: 1.5rem;
  color: #5c4a3d;
  font-weight: 300;
}

.names-display .ampersand {
  margin: 0 0.75rem;
  color: #d4af37;
  font-style: italic;
}

.section-title {
  font-size: 1.5rem;
  color: #5c4a3d;
  font-weight: 300;
  letter-spacing: 5px;
}

.rsvp-card {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(212, 175, 55, 0.3);
  border-radius: 20px;
  padding: 2rem 1.5rem;
  backdrop-filter: blur(10px);
  margin-bottom: 3rem;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.06);
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  color: #d4af37;
  font-size: 1rem;
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.form-group input[type="text"],
.form-group textarea {
  width: 100%;
  padding: 1rem;
  background: #fdfcfb;
  border: 1px solid #e0d6c8;
  border-radius: 10px;
  color: #5c4a3d;
  font-size: 1rem;
  font-family: inherit;
  transition: all 0.3s;
}

.form-group input[type="text"]:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #d4af37;
  background: #fff;
  box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.1);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: #a0917b;
}

.attendance-options {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.attendance-option {
  cursor: pointer;
}

.attendance-option input {
  display: none;
}

.option-box {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.5rem;
  background: #fdfcfb;
  border: 1px solid #e0d6c8;
  border-radius: 10px;
  transition: all 0.3s;
}

.option-box:hover {
  background: #fff;
  border-color: #d4af37;
}

.attendance-option input:checked + .option-box.attend {
  background: rgba(46, 125, 50, 0.2);
  border-color: #4caf50;
}

.attendance-option input:checked + .option-box.decline {
  background: rgba(198, 40, 40, 0.2);
  border-color: #ef5350;
}

.option-icon {
  font-size: 1.2rem;
  font-weight: 700;
}

.attend .option-icon {
  color: #4caf50;
}

.decline .option-icon {
  color: #ef5350;
}

.option-text {
  color: #5c4a3d;
  font-size: 1rem;
}

.submit-btn {
  width: 100%;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #d4af37, #f0d78c);
  color: #1a1a2e;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 700;
  font-family: inherit;
  cursor: pointer;
  transition: all 0.3s;
  margin-top: 1rem;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(212, 175, 55, 0.3);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.submit-message {
  text-align: center;
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 10px;
  background: rgba(198, 40, 40, 0.2);
  color: #ef5350;
}

.submit-message.success {
  background: rgba(46, 125, 50, 0.2);
  color: #4caf50;
}

.wishes-section {
  margin-top: 3rem;
}

.wishes-title {
  text-align: center;
  font-size: 1.5rem;
  color: #5c4a3d;
  font-weight: 400;
  margin-bottom: 1rem;
}

.scroll-hint {
  text-align: center;
  margin-bottom: 1rem;
  color: #a0917b;
}

.wishes-list {
  max-height: 400px;
  overflow-y: auto;
  padding-right: 0.5rem;
}

.wishes-list::-webkit-scrollbar {
  width: 6px;
}

.wishes-list::-webkit-scrollbar-track {
  background: rgba(212, 175, 55, 0.1);
  border-radius: 10px;
}

.wishes-list::-webkit-scrollbar-thumb {
  background: #d4af37;
  border-radius: 10px;
}

.wish-card {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(212, 175, 55, 0.2);
  border-radius: 15px;
  margin-bottom: 1rem;
  transition: all 0.3s;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.03);
}

.wish-card:hover {
  background: rgba(255, 255, 255, 1);
  transform: translateX(5px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.06);
}

.wish-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: linear-gradient(135deg, #d4af37, #f0d78c);
  color: #1a1a2e;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1rem;
  flex-shrink: 0;
}

.wish-content {
  flex: 1;
}

.wish-name {
  color: #5c4a3d;
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.wish-text {
  color: #6b5b4f;
  font-size: 0.95rem;
  line-height: 1.6;
}
</style>

