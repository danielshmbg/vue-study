<template>
  <section class="wedding-timeline">
    <div class="container">
      <h2 class="section-title">Event Timeline</h2>
      <p class="section-subtitle">Here's what to expect on our special day</p>

      <div class="timeline">
        <div 
          v-for="(event, index) in events" 
          :key="index" 
          class="timeline-item"
          :class="{ 'timeline-item-right': index % 2 !== 0 }"
        >
          <div class="timeline-marker">
            <div class="timeline-icon">{{ event.icon }}</div>
          </div>
          <div class="timeline-content">
            <div class="timeline-time">{{ event.time }}</div>
            <h3 class="timeline-title">{{ event.title }}</h3>
            <p class="timeline-description">{{ event.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingTimeline',
  data() {
    return {
      events: [
        {
          time: '3:30 PM',
          title: 'Guest Arrival',
          description: 'Please arrive early to find your seats and enjoy the pre-ceremony music.',
          icon: '🚗'
        },
        {
          time: '4:00 PM',
          title: 'Ceremony Begins',
          description: 'The wedding ceremony begins at St. Mary\'s Cathedral.',
          icon: '💒'
        },
        {
          time: '5:00 PM',
          title: 'Cocktail Hour',
          description: 'Join us for cocktails and hors d\'oeuvres while we take photos.',
          icon: '🍸'
        },
        {
          time: '6:00 PM',
          title: 'Reception Entrance',
          description: 'Grand entrance of the newlyweds at The Grand Ballroom.',
          icon: '🎉'
        },
        {
          time: '6:30 PM',
          title: 'Dinner Service',
          description: 'A delicious three-course meal prepared by our chefs.',
          icon: '🍽️'
        },
        {
          time: '8:00 PM',
          title: 'First Dance & Toasts',
          description: 'First dance followed by heartfelt speeches from our loved ones.',
          icon: '💃'
        },
        {
          time: '8:30 PM',
          title: 'Cake Cutting',
          description: 'Traditional cake cutting ceremony.',
          icon: '🎂'
        },
        {
          time: '9:00 PM',
          title: 'Dance Party',
          description: 'Let\'s dance the night away! DJ will keep the party going.',
          icon: '🎵'
        },
        {
          time: '11:00 PM',
          title: 'Grand Exit',
          description: 'Sparkler send-off for the happy couple.',
          icon: '✨'
        }
      ]
    }
  }
}
</script>

<style scoped>
.wedding-timeline {
  padding: 5rem 0;
  background: linear-gradient(to bottom, #ffffff 0%, #f8f9fa 100%);
}

.container {
  max-width: 1000px;
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
  color: #666;
  font-size: 1.1rem;
  margin-bottom: 4rem;
  font-style: italic;
}

.timeline {
  position: relative;
  padding: 2rem 0;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, #d4af37, #f0e68c, #d4af37);
  transform: translateX(-50%);
}

.timeline-item {
  position: relative;
  margin-bottom: 3rem;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: calc(50% + 40px);
}

.timeline-item-right {
  justify-content: flex-start;
  padding-right: 0;
  padding-left: calc(50% + 40px);
}

.timeline-marker {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 60px;
  background: white;
  border: 3px solid #d4af37;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.1);
}

.timeline-icon {
  font-size: 1.8rem;
}

.timeline-content {
  background: white;
  padding: 1.5rem 2rem;
  border-radius: 10px;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.08);
  max-width: 400px;
  border-left: 4px solid #d4af37;
  transition: transform 0.3s, box-shadow 0.3s;
}

.timeline-item-right .timeline-content {
  border-left: none;
  border-right: 4px solid #d4af37;
}

.timeline-content:hover {
  transform: scale(1.02);
  box-shadow: 0 5px 25px rgba(212, 175, 55, 0.15);
}

.timeline-time {
  font-size: 1.1rem;
  color: #d4af37;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.timeline-title {
  font-family: 'Georgia', serif;
  font-size: 1.3rem;
  color: #2c3e50;
  margin-bottom: 0.5rem;
  font-weight: 400;
}

.timeline-description {
  color: #666;
  line-height: 1.6;
  font-size: 0.95rem;
}

@media (max-width: 768px) {
  .timeline::before {
    left: 30px;
  }

  .timeline-item,
  .timeline-item-right {
    padding-right: 0;
    padding-left: 70px;
    justify-content: flex-start;
  }

  .timeline-marker {
    left: 30px;
    width: 50px;
    height: 50px;
  }

  .timeline-icon {
    font-size: 1.5rem;
  }

  .timeline-content {
    max-width: 100%;
  }

  .timeline-item-right .timeline-content {
    border-left: 4px solid #d4af37;
    border-right: none;
  }

  .section-title {
    font-size: 2rem;
  }
}
</style>

