<template>
  <section class="wedding-rsvp">
    <div class="container">
      <h2 class="section-title">RSVP</h2>
      <p class="section-subtitle">Please respond by May 1st, 2026</p>

      <div class="rsvp-container">
        <form @submit.prevent="handleSubmit" class="rsvp-form">
          <div class="form-group">
            <label for="name">Full Name *</label>
            <input 
              type="text" 
              id="name" 
              v-model="formData.name" 
              required
              placeholder="Enter your full name"
            >
          </div>

          <div class="form-group">
            <label for="email">Email Address *</label>
            <input 
              type="email" 
              id="email" 
              v-model="formData.email" 
              required
              placeholder="your.email@example.com"
            >
          </div>

          <div class="form-group">
            <label for="phone">Phone Number</label>
            <input 
              type="tel" 
              id="phone" 
              v-model="formData.phone"
              placeholder="(123) 456-7890"
            >
          </div>

          <div class="form-group">
            <label>Will you be attending? *</label>
            <div class="radio-group">
              <label class="radio-label">
                <input 
                  type="radio" 
                  value="yes" 
                  v-model="formData.attending" 
                  required
                >
                <span class="radio-text">✓ Joyfully Accept</span>
              </label>
              <label class="radio-label">
                <input 
                  type="radio" 
                  value="no" 
                  v-model="formData.attending" 
                  required
                >
                <span class="radio-text">✗ Regretfully Decline</span>
              </label>
            </div>
          </div>

          <div v-if="formData.attending === 'yes'" class="form-group">
            <label for="guests">Number of Guests *</label>
            <select id="guests" v-model="formData.guests" required>
              <option value="">Select number of guests</option>
              <option value="1">1 Guest</option>
              <option value="2">2 Guests</option>
              <option value="3">3 Guests</option>
              <option value="4">4 Guests</option>
            </select>
          </div>

          <div v-if="formData.attending === 'yes'" class="form-group">
            <label for="dietary">Dietary Restrictions</label>
            <textarea 
              id="dietary" 
              v-model="formData.dietary" 
              rows="3"
              placeholder="Please let us know about any dietary restrictions or allergies"
            ></textarea>
          </div>

          <div class="form-group">
            <label for="message">Message to the Couple</label>
            <textarea 
              id="message" 
              v-model="formData.message" 
              rows="4"
              placeholder="Share your well wishes or any special requests"
            ></textarea>
          </div>

          <button type="submit" class="submit-button">
            <span v-if="!isSubmitting">Send RSVP 💌</span>
            <span v-else>Sending...</span>
          </button>

          <p v-if="submitMessage" class="submit-message" :class="{ success: isSuccess }">
            {{ submitMessage }}
          </p>
        </form>

        <div class="rsvp-info">
          <div class="info-card">
            <h3>Need Help?</h3>
            <p>If you have any questions or need to make changes to your RSVP, please contact us:</p>
            <div class="contact-info">
              <p>📧 wedding@emilyandtjames.com</p>
              <p>📱 (555) 123-4567</p>
            </div>
          </div>

          <div class="info-card">
            <h3>Important Notes</h3>
            <ul class="notes-list">
              <li>Please RSVP by May 1st, 2026</li>
              <li>Each invitation includes specific guest count</li>
              <li>Children are welcome</li>
              <li>The venue is wheelchair accessible</li>
              <li>Please arrive 30 minutes early</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingRSVP',
  data() {
    return {
      formData: {
        name: '',
        email: '',
        phone: '',
        attending: '',
        guests: '',
        dietary: '',
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

      // In production, this would send data to a backend
      console.log('RSVP Data:', this.formData)

      this.isSubmitting = false
      this.isSuccess = true
      this.submitMessage = 'Thank you! Your RSVP has been received. We can\'t wait to celebrate with you! 🎉'

      // Reset form after 3 seconds
      setTimeout(() => {
        this.formData = {
          name: '',
          email: '',
          phone: '',
          attending: '',
          guests: '',
          dietary: '',
          message: ''
        }
        this.submitMessage = ''
        this.isSuccess = false
      }, 5000)
    }
  }
}
</script>

<style scoped>
.wedding-rsvp {
  padding: 5rem 0;
  background-color: #ffffff;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-title {
  font-family: 'Georgia', serif;
  font-size: 2.5rem;
  color: #2c3e50;
  text-align: center;
  margin-bottom: 1rem;
  font-weight: 300;
}

.section-subtitle {
  text-align: center;
  color: #d4af37;
  font-size: 1.2rem;
  margin-bottom: 3rem;
  font-weight: 600;
}

.rsvp-container {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 3rem;
}

.rsvp-form {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: 3rem;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
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

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  font-family: inherit;
  transition: border-color 0.3s, box-shadow 0.3s;
  background: white;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #d4af37;
  box-shadow: 0 0 0 3px rgba(212, 175, 55, 0.1);
}

.radio-group {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.radio-label {
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 0.75rem 1.5rem;
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  transition: all 0.3s;
  flex: 1;
  min-width: 150px;
}

.radio-label:hover {
  border-color: #d4af37;
}

.radio-label input {
  margin-right: 0.5rem;
  width: auto;
}

.radio-label input:checked + .radio-text {
  color: #d4af37;
  font-weight: 700;
}

.radio-label:has(input:checked) {
  background: rgba(212, 175, 55, 0.1);
  border-color: #d4af37;
}

.submit-button {
  width: 100%;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #d4af37, #f0e68c);
  color: #2c3e50;
  border: none;
  border-radius: 8px;
  font-size: 1.2rem;
  font-weight: 700;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
  margin-top: 1rem;
}

.submit-button:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 5px 20px rgba(212, 175, 55, 0.3);
}

.submit-button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.submit-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  background: #ffe0e0;
  color: #c00;
  font-weight: 600;
}

.submit-message.success {
  background: #d4edda;
  color: #155724;
}

.rsvp-info {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.info-card {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
}

.info-card h3 {
  font-family: 'Georgia', serif;
  font-size: 1.5rem;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-weight: 400;
}

.info-card p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.contact-info {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  margin-top: 1rem;
}

.contact-info p {
  margin: 0.5rem 0;
  color: #2c3e50;
  font-weight: 600;
}

.notes-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.notes-list li {
  padding: 0.5rem 0;
  padding-left: 1.5rem;
  position: relative;
  color: #666;
  line-height: 1.6;
}

.notes-list li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: #d4af37;
  font-weight: 700;
}

@media (max-width: 968px) {
  .rsvp-container {
    grid-template-columns: 1fr;
  }

  .rsvp-form {
    padding: 2rem;
  }
}

@media (max-width: 768px) {
  .wedding-rsvp {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .radio-group {
    flex-direction: column;
  }

  .radio-label {
    min-width: auto;
  }
}
</style>

