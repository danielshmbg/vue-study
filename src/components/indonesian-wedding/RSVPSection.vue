<template>
  <section class="rsvp-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">RSVP</h2>
        <p class="section-subtitle">Please let us know if you can join us</p>
      </div>

      <div class="rsvp-form-container">
        <form @submit.prevent="handleSubmit" class="rsvp-form">
          <div class="form-group">
            <label for="guest-name">Full Name *</label>
            <input 
              type="text" 
              id="guest-name" 
              v-model="formData.name" 
              required
              placeholder="Enter your name"
            >
          </div>

          <div class="form-group">
            <label for="guest-email">Email Address</label>
            <input 
              type="email" 
              id="guest-email" 
              v-model="formData.email"
              placeholder="your.email@example.com"
            >
          </div>

          <div class="form-group">
            <label>Will you attend? *</label>
            <div class="radio-options">
              <label class="radio-option">
                <input 
                  type="radio" 
                  value="yes" 
                  v-model="formData.attending" 
                  required
                >
                <span class="radio-label">
                  <span class="radio-icon">✓</span>
                  Sure, I'll be there!
                </span>
              </label>
              <label class="radio-option">
                <input 
                  type="radio" 
                  value="no" 
                  v-model="formData.attending" 
                  required
                >
                <span class="radio-label">
                  <span class="radio-icon">✗</span>
                  Sorry, I can't attend
                </span>
              </label>
            </div>
          </div>

          <div v-if="formData.attending === 'yes'" class="form-group">
            <label>Which event will you attend? *</label>
            <div class="checkbox-options">
              <label class="checkbox-option">
                <input 
                  type="checkbox" 
                  value="ceremony" 
                  v-model="formData.events"
                >
                <span>💒 Holy Matrimony</span>
              </label>
              <label class="checkbox-option">
                <input 
                  type="checkbox" 
                  value="reception" 
                  v-model="formData.events"
                >
                <span>🥂 Reception</span>
              </label>
              <label class="checkbox-option">
                <input 
                  type="checkbox" 
                  value="all" 
                  v-model="formData.events"
                >
                <span>🎉 Attend All</span>
              </label>
            </div>
          </div>

          <div v-if="formData.attending === 'yes'" class="form-group">
            <label for="guest-count">How many guests? *</label>
            <select id="guest-count" v-model="formData.guestCount" required>
              <option value="">Select number</option>
              <option value="1">1 Guest</option>
              <option value="2">2 Guests</option>
              <option value="3">3 Guests</option>
              <option value="4">4 Guests</option>
            </select>
          </div>

          <div class="form-group">
            <label for="message">Message (Optional)</label>
            <textarea 
              id="message" 
              v-model="formData.message" 
              rows="4"
              placeholder="Leave your wishes or any special requirements..."
            ></textarea>
          </div>

          <button type="submit" class="submit-btn" :disabled="isSubmitting">
            <span v-if="!isSubmitting">Confirm RSVP ✉️</span>
            <span v-else">Sending...</span>
          </button>

          <p v-if="submitMessage" class="submit-message" :class="{ success: isSuccess }">
            {{ submitMessage }}
          </p>
        </form>

        <div class="rsvp-info">
          <div class="info-box">
            <h3>📍 Location Details</h3>
            <p>Both ceremony and reception venues are wheelchair accessible with parking available.</p>
          </div>
          <div class="info-box">
            <h3>⏰ Important Dates</h3>
            <p>Please RSVP by <strong>November 20th, 2025</strong></p>
            <p>Kindly arrive 30 minutes before ceremony starts</p>
          </div>
          <div class="info-box">
            <h3>📞 Contact Us</h3>
            <p>For questions or concerns:</p>
            <p><strong>Sarah:</strong> +1 (555) 123-4567</p>
            <p><strong>Michael:</strong> +1 (555) 765-4321</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'RSVPSection',
  data() {
    return {
      formData: {
        name: '',
        email: '',
        attending: '',
        events: [],
        guestCount: '',
        message: ''
      },
      isSubmitting: false,
      submitMessage: '',
      isSuccess: false
    }
  },
  methods: {
    async handleSubmit() {
      this.isSubmitting = true
      this.submitMessage = ''

      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1500))

      console.log('RSVP Data:', this.formData)

      this.isSubmitting = false
      this.isSuccess = true
      this.submitMessage = 'Thank you for your RSVP! We\'ve received your response. 🎉'

      // Reset form after 4 seconds
      setTimeout(() => {
        this.formData = {
          name: '',
          email: '',
          attending: '',
          events: [],
          guestCount: '',
          message: ''
        }
        this.submitMessage = ''
        this.isSuccess = false
      }, 4000)
    }
  }
}
</script>

<style scoped>
.rsvp-section {
  padding: 5rem 0;
  background: linear-gradient(to bottom, #f8f9fa 0%, #ffffff 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-title {
  font-family: 'Georgia', serif;
  font-size: clamp(2rem, 5vw, 3rem);
  color: #764ba2;
  margin-bottom: 0.5rem;
  font-weight: 400;
}

.section-subtitle {
  font-size: 1.1rem;
  color: #666;
}

.rsvp-form-container {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 3rem;
}

.rsvp-form {
  background: white;
  padding: 3rem;
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.08);
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  color: #2c3e50;
  font-weight: 600;
  margin-bottom: 0.5rem;
  font-size: 1rem;
}

.form-group input[type="text"],
.form-group input[type="email"],
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 1rem;
  font-family: inherit;
  transition: all 0.3s;
  background: #fafafa;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #764ba2;
  background: white;
  box-shadow: 0 0 0 3px rgba(118, 75, 162, 0.1);
}

.radio-options,
.checkbox-options {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.radio-option,
.checkbox-option {
  display: flex;
  align-items: center;
  padding: 1rem 1.5rem;
  background: #fafafa;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s;
}

.radio-option:hover,
.checkbox-option:hover {
  border-color: #764ba2;
  background: white;
}

.radio-option input,
.checkbox-option input {
  margin-right: 1rem;
  width: auto;
  cursor: pointer;
}

.radio-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1.05rem;
}

.radio-icon {
  font-weight: 700;
  color: #764ba2;
}

.radio-option:has(input:checked),
.checkbox-option:has(input:checked) {
  background: rgba(118, 75, 162, 0.1);
  border-color: #764ba2;
}

.submit-btn {
  width: 100%;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1.2rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s;
  margin-top: 1rem;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(118, 75, 162, 0.3);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.submit-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 10px;
  text-align: center;
  font-weight: 600;
  background: #ffe0e0;
  color: #c00;
}

.submit-message.success {
  background: #d4edda;
  color: #155724;
}

.rsvp-info {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.info-box {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
}

.info-box h3 {
  color: #764ba2;
  font-size: 1.3rem;
  margin-bottom: 1rem;
  font-weight: 600;
}

.info-box p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 0.5rem;
}

.info-box strong {
  color: #2c3e50;
}

@media (max-width: 968px) {
  .rsvp-form-container {
    grid-template-columns: 1fr;
  }

  .rsvp-form {
    padding: 2rem;
  }
}

@media (max-width: 768px) {
  .rsvp-section {
    padding: 3rem 0;
  }

  .radio-options {
    gap: 0.75rem;
  }

  .radio-option,
  .checkbox-option {
    padding: 0.75rem 1rem;
  }
}
</style>

