<template>
  <section class="wishes-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Wedding Wishes</h2>
        <p class="section-subtitle">
          Leave us your beautiful wishes & prayers here as we are excited to embark on this new journey together ❤️
        </p>
      </div>

      <div class="wishes-container">
        <form @submit.prevent="submitWish" class="wish-form">
          <div class="form-group">
            <input 
              type="text" 
              v-model="newWish.name" 
              placeholder="Your Name *"
              required
              class="wish-input"
            >
          </div>

          <div class="form-group">
            <textarea 
              v-model="newWish.message" 
              placeholder="Write your wishes and prayers... *"
              rows="4"
              required
              class="wish-textarea"
            ></textarea>
          </div>

          <button type="submit" class="send-wish-btn" :disabled="isSubmitting">
            <span v-if="!isSubmitting">Send Wishes 💌</span>
            <span v-else>Sending...</span>
          </button>

          <p v-if="wishMessage" class="wish-message" :class="{ success: wishSuccess }">
            {{ wishMessage }}
          </p>
        </form>

        <div class="wishes-list">
          <h3 class="wishes-list-title">Messages from Guests ({{ wishes.length }})</h3>
          
          <div class="wishes-scroll">
            <div 
              v-for="(wish, index) in wishes" 
              :key="index" 
              class="wish-card"
            >
              <div class="wish-header">
                <div class="wish-avatar">{{ getInitials(wish.name) }}</div>
                <div class="wish-info">
                  <h4 class="wish-name">{{ wish.name }}</h4>
                  <p class="wish-date">{{ wish.date }}</p>
                </div>
              </div>
              <p class="wish-text">{{ wish.message }}</p>
            </div>

            <div v-if="wishes.length === 0" class="no-wishes">
              <p>🎉 Be the first to leave a message!</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WishesSection',
  data() {
    return {
      newWish: {
        name: '',
        message: ''
      },
      isSubmitting: false,
      wishMessage: '',
      wishSuccess: false,
      wishes: [
        {
          name: 'Jessica Williams',
          message: 'Congratulations! Wishing you both a lifetime of love and happiness. Can\'t wait to celebrate with you! 🎉',
          date: 'November 15, 2025'
        },
        {
          name: 'David Thompson',
          message: 'So happy for you both! May your marriage be filled with joy, laughter, and endless love. Congratulations!',
          date: 'November 14, 2025'
        },
        {
          name: 'Maria Garcia',
          message: 'What wonderful news! Wishing you all the best as you begin this beautiful journey together. Much love! ❤️',
          date: 'November 13, 2025'
        }
      ]
    }
  },
  methods: {
    getInitials(name) {
      return name
        .split(' ')
        .map(word => word[0])
        .join('')
        .toUpperCase()
        .substring(0, 2)
    },
    async submitWish() {
      this.isSubmitting = true
      this.wishMessage = ''

      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1000))

      // Add new wish to the list
      const newWishData = {
        name: this.newWish.name,
        message: this.newWish.message,
        date: new Date().toLocaleDateString('en-US', {
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        })
      }

      this.wishes.unshift(newWishData)

      this.isSubmitting = false
      this.wishSuccess = true
      this.wishMessage = 'Thank you for your beautiful wishes! 💕'

      // Reset form
      setTimeout(() => {
        this.newWish = {
          name: '',
          message: ''
        }
        this.wishMessage = ''
        this.wishSuccess = false
      }, 3000)
    }
  }
}
</script>

<style scoped>
.wishes-section {
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
  margin-bottom: 1rem;
  font-weight: 400;
}

.section-subtitle {
  font-size: 1.05rem;
  color: #666;
  line-height: 1.7;
  max-width: 700px;
  margin: 0 auto;
}

.wishes-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
}

.wish-form {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.08);
  height: fit-content;
  position: sticky;
  top: 2rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.wish-input,
.wish-textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 1rem;
  font-family: inherit;
  transition: all 0.3s;
  background: #fafafa;
}

.wish-input:focus,
.wish-textarea:focus {
  outline: none;
  border-color: #764ba2;
  background: white;
  box-shadow: 0 0 0 3px rgba(118, 75, 162, 0.1);
}

.send-wish-btn {
  width: 100%;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s;
}

.send-wish-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(118, 75, 162, 0.3);
}

.send-wish-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.wish-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 10px;
  text-align: center;
  font-weight: 600;
  background: #ffe0e0;
  color: #c00;
}

.wish-message.success {
  background: #d4edda;
  color: #155724;
}

.wishes-list-title {
  color: #2c3e50;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  font-weight: 600;
}

.wishes-scroll {
  max-height: 600px;
  overflow-y: auto;
  padding-right: 0.5rem;
}

.wishes-scroll::-webkit-scrollbar {
  width: 8px;
}

.wishes-scroll::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

.wishes-scroll::-webkit-scrollbar-thumb {
  background: #764ba2;
  border-radius: 10px;
}

.wishes-scroll::-webkit-scrollbar-thumb:hover {
  background: #667eea;
}

.wish-card {
  background: white;
  padding: 1.5rem;
  border-radius: 15px;
  margin-bottom: 1rem;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s, box-shadow 0.3s;
}

.wish-card:hover {
  transform: translateX(5px);
  box-shadow: 0 5px 20px rgba(118, 75, 162, 0.15);
}

.wish-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.wish-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1.1rem;
  flex-shrink: 0;
}

.wish-info {
  flex: 1;
}

.wish-name {
  color: #2c3e50;
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.wish-date {
  color: #999;
  font-size: 0.85rem;
}

.wish-text {
  color: #666;
  line-height: 1.6;
  font-size: 0.95rem;
}

.no-wishes {
  text-align: center;
  padding: 3rem 2rem;
  color: #999;
  font-size: 1.1rem;
}

@media (max-width: 968px) {
  .wishes-container {
    grid-template-columns: 1fr;
  }

  .wish-form {
    position: static;
  }

  .wishes-scroll {
    max-height: 400px;
  }
}

@media (max-width: 768px) {
  .wishes-section {
    padding: 3rem 0;
  }

  .wish-form {
    padding: 2rem 1.5rem;
  }

  .wishes-scroll {
    max-height: 300px;
  }
}
</style>

