<template>
  <section class="gift-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Wedding Gift</h2>
        <p class="section-subtitle">
          Your blessing and coming to our wedding are enough for us. However, if you want to give a gift 
          we provide a Digital Envelope to make it easier for you. Thank you 🙏
        </p>
      </div>

      <div class="gift-container">
        <div class="bank-selection">
          <label>Select Bank</label>
          <div class="bank-options">
            <button 
              v-for="bank in banks" 
              :key="bank.id"
              @click="selectBank(bank.id)"
              class="bank-btn"
              :class="{ active: selectedBank === bank.id }"
            >
              <span class="bank-icon">{{ bank.icon }}</span>
              <span class="bank-name">{{ bank.name }}</span>
            </button>
          </div>
        </div>

        <div v-if="selectedBank" class="bank-details">
          <div class="account-info">
            <h3>Account Details</h3>
            <div class="info-row">
              <span class="info-label">Bank Name:</span>
              <span class="info-value">{{ currentBank.name }}</span>
            </div>
            <div class="info-row">
              <span class="info-label">Account Number:</span>
              <div class="copy-container">
                <span class="info-value account-number">{{ currentBank.accountNumber }}</span>
                <button @click="copyAccountNumber" class="copy-btn">
                  {{ copied ? '✓ Copied!' : '📋 Copy' }}
                </button>
              </div>
            </div>
            <div class="info-row">
              <span class="info-label">Account Name:</span>
              <span class="info-value">{{ currentBank.accountName }}</span>
            </div>
          </div>

          <div class="gift-form">
            <div class="form-group">
              <label for="amount">Amount</label>
              <input 
                type="number" 
                id="amount" 
                v-model="giftData.amount"
                placeholder="Enter amount"
                min="0"
              >
            </div>

            <div class="form-group">
              <label for="proof">Upload Proof of Transfer</label>
              <input 
                type="file" 
                id="proof" 
                @change="handleFileUpload"
                accept="image/*"
                class="file-input"
              >
              <p v-if="giftData.fileName" class="file-name">📎 {{ giftData.fileName }}</p>
            </div>

            <button @click="submitGift" class="submit-gift-btn" :disabled="isSubmittingGift">
              <span v-if="!isSubmittingGift">Submit Gift 🎁</span>
              <span v-else>Submitting...</span>
            </button>

            <p v-if="giftMessage" class="gift-message" :class="{ success: giftSuccess }">
              {{ giftMessage }}
            </p>
          </div>
        </div>

        <div v-else class="no-bank-selected">
          <p>👆 Please select a bank to see account details</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'GiftSection',
  data() {
    return {
      banks: [
        {
          id: 'bca',
          name: 'Bank Central Asia (BCA)',
          icon: '🏦',
          accountNumber: '1234567890',
          accountName: 'Sarah Anderson & Michael Chen'
        },
        {
          id: 'bni',
          name: 'Bank Negara Indonesia (BNI)',
          icon: '🏦',
          accountNumber: '0987654321',
          accountName: 'Sarah Anderson & Michael Chen'
        },
        {
          id: 'mandiri',
          name: 'Bank Mandiri',
          icon: '🏦',
          accountNumber: '5678901234',
          accountName: 'Sarah Anderson & Michael Chen'
        }
      ],
      selectedBank: null,
      copied: false,
      giftData: {
        amount: '',
        fileName: ''
      },
      isSubmittingGift: false,
      giftMessage: '',
      giftSuccess: false
    }
  },
  computed: {
    currentBank() {
      return this.banks.find(bank => bank.id === this.selectedBank)
    }
  },
  methods: {
    selectBank(bankId) {
      this.selectedBank = bankId
      this.copied = false
    },
    async copyAccountNumber() {
      if (this.currentBank) {
        try {
          await navigator.clipboard.writeText(this.currentBank.accountNumber)
          this.copied = true
          setTimeout(() => {
            this.copied = false
          }, 2000)
        } catch (err) {
          alert(`Account Number: ${this.currentBank.accountNumber}`)
        }
      }
    },
    handleFileUpload(event) {
      const file = event.target.files[0]
      if (file) {
        this.giftData.fileName = file.name
      }
    },
    async submitGift() {
      if (!this.giftData.amount) {
        this.giftMessage = 'Please enter an amount'
        this.giftSuccess = false
        return
      }

      this.isSubmittingGift = true
      this.giftMessage = ''

      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1500))

      console.log('Gift Data:', {
        bank: this.currentBank.name,
        amount: this.giftData.amount,
        file: this.giftData.fileName
      })

      this.isSubmittingGift = false
      this.giftSuccess = true
      this.giftMessage = 'Thank you for your generous gift! 🎁 We truly appreciate it.'

      // Reset after 4 seconds
      setTimeout(() => {
        this.giftData = {
          amount: '',
          fileName: ''
        }
        this.giftMessage = ''
        this.giftSuccess = false
      }, 4000)
    }
  }
}
</script>

<style scoped>
.gift-section {
  padding: 5rem 0;
  background: linear-gradient(to bottom, #ffffff 0%, #f8f9fa 100%);
}

.container {
  max-width: 900px;
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

.gift-container {
  background: white;
  padding: 3rem;
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.08);
}

.bank-selection label {
  display: block;
  color: #2c3e50;
  font-weight: 700;
  margin-bottom: 1rem;
  font-size: 1.1rem;
}

.bank-options {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}

.bank-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 1.5rem;
  background: #fafafa;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s;
  font-family: inherit;
}

.bank-btn:hover {
  border-color: #764ba2;
  background: white;
  transform: translateY(-2px);
}

.bank-btn.active {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-color: #764ba2;
}

.bank-icon {
  font-size: 1.5rem;
}

.bank-name {
  font-size: 0.95rem;
  font-weight: 600;
}

.bank-details {
  border-top: 2px solid #f0f0f0;
  padding-top: 2rem;
}

.account-info {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: 2rem;
  border-radius: 15px;
  margin-bottom: 2rem;
}

.account-info h3 {
  color: #764ba2;
  font-size: 1.3rem;
  margin-bottom: 1.5rem;
  font-weight: 600;
}

.info-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  gap: 1rem;
}

.info-label {
  color: #666;
  font-weight: 600;
}

.info-value {
  color: #2c3e50;
  font-weight: 700;
  font-size: 1.05rem;
}

.copy-container {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.account-number {
  font-family: monospace;
  font-size: 1.1rem;
}

.copy-btn {
  padding: 0.5rem 1rem;
  background: #764ba2;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all 0.3s;
  white-space: nowrap;
}

.copy-btn:hover {
  background: #667eea;
}

.gift-form {
  margin-top: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  color: #2c3e50;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.form-group input[type="number"],
.form-group input[type="file"] {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 1rem;
  font-family: inherit;
  transition: all 0.3s;
  background: #fafafa;
}

.form-group input:focus {
  outline: none;
  border-color: #764ba2;
  background: white;
  box-shadow: 0 0 0 3px rgba(118, 75, 162, 0.1);
}

.file-input {
  cursor: pointer;
}

.file-name {
  margin-top: 0.5rem;
  color: #666;
  font-size: 0.95rem;
}

.submit-gift-btn {
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
}

.submit-gift-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(118, 75, 162, 0.3);
}

.submit-gift-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.gift-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 10px;
  text-align: center;
  font-weight: 600;
  background: #ffe0e0;
  color: #c00;
}

.gift-message.success {
  background: #d4edda;
  color: #155724;
}

.no-bank-selected {
  text-align: center;
  padding: 3rem 2rem;
  color: #999;
  font-size: 1.1rem;
}

@media (max-width: 768px) {
  .gift-section {
    padding: 3rem 0;
  }

  .gift-container {
    padding: 2rem 1.5rem;
  }

  .bank-options {
    grid-template-columns: 1fr;
  }

  .info-row {
    flex-direction: column;
    align-items: flex-start;
  }

  .copy-container {
    width: 100%;
    justify-content: space-between;
  }
}
</style>

