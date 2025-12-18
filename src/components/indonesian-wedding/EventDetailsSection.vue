<template>
  <section class="event-details-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Save the Date</h2>
        <div class="wedding-date-display">{{ weddingDateFormatted }}</div>
      </div>

      <div class="countdown-container">
        <div class="countdown-item" v-for="unit in countdownUnits" :key="unit.label">
          <div class="countdown-value">{{ countdown[unit.key] }}</div>
          <div class="countdown-label">{{ unit.label }}</div>
        </div>
      </div>

      <div class="add-calendar-btn-container">
        <button class="add-calendar-btn" @click="addToCalendar">
          📅 Add to Calendar
        </button>
      </div>

      <div class="events-grid">
        <div class="event-card" v-for="(event, index) in events" :key="index">
          <div class="event-icon">{{ event.icon }}</div>
          <h3 class="event-title">{{ event.title }}</h3>
          <div class="event-detail">
            <span class="detail-icon">📅</span>
            <span>{{ event.date }}</span>
          </div>
          <div class="event-detail">
            <span class="detail-icon">🕐</span>
            <span>{{ event.time }}</span>
          </div>
          <div class="event-detail">
            <span class="detail-icon">📍</span>
            <span>{{ event.venue }}</span>
          </div>
          <p class="event-address">{{ event.address }}</p>
          <button class="view-map-btn" @click="openMap(event.mapUrl)">
            View Map 🗺️
          </button>
        </div>
      </div>

      <div class="important-note">
        <div class="note-icon">⚠️</div>
        <div class="note-content">
          <p class="note-title">Important Note</p>
          <p class="note-text">{{ importantNote }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'EventDetailsSection',
  data() {
    return {
      weddingDate: new Date('2025-12-20T14:00:00'),
      countdown: {
        days: 0,
        hours: 0,
        minutes: 0,
        seconds: 0
      },
      countdownUnits: [
        { key: 'days', label: 'Days' },
        { key: 'hours', label: 'Hours' },
        { key: 'minutes', label: 'Minutes' },
        { key: 'seconds', label: 'Seconds' }
      ],
      events: [
        {
          icon: '💒',
          title: 'Holy Matrimony',
          date: 'Saturday, December 20th, 2025',
          time: '2:00 PM - 3:30 PM',
          venue: 'Grace Cathedral',
          address: '789 Cathedral Lane, Downtown, State 12345',
          mapUrl: 'https://maps.google.com'
        },
        {
          icon: '🥂',
          title: 'Wedding Reception',
          date: 'Saturday, December 20th, 2025',
          time: '5:00 PM - 10:00 PM',
          venue: 'The Grand Ballroom Hotel',
          address: '456 Celebration Avenue, Downtown, State 12345',
          mapUrl: 'https://maps.google.com'
        }
      ],
      importantNote: 'We love your little ones, but this event is for Adults-only. Thank you for understanding and celebrating this day with us.',
      countdownInterval: null
    }
  },
  computed: {
    weddingDateFormatted() {
      return this.weddingDate.toLocaleDateString('en-US', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })
    }
  },
  mounted() {
    this.updateCountdown()
    this.countdownInterval = setInterval(this.updateCountdown, 1000)
  },
  beforeUnmount() {
    if (this.countdownInterval) {
      clearInterval(this.countdownInterval)
    }
  },
  methods: {
    updateCountdown() {
      const now = new Date().getTime()
      const distance = this.weddingDate.getTime() - now

      if (distance > 0) {
        this.countdown.days = Math.floor(distance / (1000 * 60 * 60 * 24))
        this.countdown.hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
        this.countdown.minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60))
        this.countdown.seconds = Math.floor((distance % (1000 * 60)) / 1000)
      } else {
        this.countdown = { days: 0, hours: 0, minutes: 0, seconds: 0 }
      }
    },
    addToCalendar() {
      alert('Calendar integration would open here!\n\nIn production, this would open your calendar app or download an .ics file.')
    },
    openMap(url) {
      alert(`Opening map...\n\nIn production, this would open: ${url}`)
    }
  }
}
</script>

<style scoped>
.event-details-section {
  padding: 5rem 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
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
  margin-bottom: 1rem;
  font-weight: 400;
}

.wedding-date-display {
  font-size: 1.5rem;
  font-weight: 600;
  opacity: 0.95;
}

.countdown-container {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.countdown-item {
  text-align: center;
  background: rgba(255, 255, 255, 0.15);
  padding: 1.5rem 2rem;
  border-radius: 15px;
  min-width: 100px;
  backdrop-filter: blur(10px);
}

.countdown-value {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1;
}

.countdown-label {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-top: 0.5rem;
  opacity: 0.9;
}

.add-calendar-btn-container {
  text-align: center;
  margin-bottom: 4rem;
}

.add-calendar-btn {
  padding: 1rem 2.5rem;
  background: white;
  color: #764ba2;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
}

.add-calendar-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
}

.events-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 3rem;
}

.event-card {
  background: white;
  color: #2c3e50;
  padding: 2.5rem 2rem;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s;
}

.event-card:hover {
  transform: translateY(-10px);
}

.event-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
}

.event-title {
  font-family: 'Georgia', serif;
  font-size: 1.8rem;
  color: #764ba2;
  margin-bottom: 1.5rem;
  font-weight: 400;
}

.event-detail {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 0.75rem;
  font-size: 1rem;
}

.detail-icon {
  font-size: 1.2rem;
}

.event-address {
  color: #666;
  font-size: 0.95rem;
  margin: 1rem 0 1.5rem;
  line-height: 1.5;
}

.view-map-btn {
  padding: 0.75rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
}

.view-map-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(118, 75, 162, 0.3);
}

.important-note {
  display: flex;
  gap: 1.5rem;
  align-items: flex-start;
  background: rgba(255, 255, 255, 0.15);
  padding: 2rem;
  border-radius: 15px;
  backdrop-filter: blur(10px);
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.note-icon {
  font-size: 2.5rem;
  flex-shrink: 0;
}

.note-title {
  font-size: 1.2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.note-text {
  line-height: 1.6;
  opacity: 0.95;
}

@media (max-width: 768px) {
  .event-details-section {
    padding: 3rem 0;
  }

  .countdown-container {
    gap: 1rem;
  }

  .countdown-item {
    padding: 1rem 1.5rem;
    min-width: 80px;
  }

  .countdown-value {
    font-size: 2rem;
  }

  .countdown-label {
    font-size: 0.75rem;
  }

  .events-grid {
    grid-template-columns: 1fr;
  }

  .important-note {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>

