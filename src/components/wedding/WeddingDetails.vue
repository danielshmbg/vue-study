<template>
  <section class="wedding-details">
    <div class="container">
      <div class="intro-text">
        <div class="decorative-line"></div>
        <h2 class="section-title">We're Getting Married!</h2>
        <div class="decorative-line"></div>
      </div>
      
      <p class="invitation-text">
        Together with our families, we joyfully invite you to celebrate our wedding day.
        Your presence would mean the world to us as we begin this new chapter of our lives together.
      </p>

      <div class="details-grid">
        <div class="detail-card detail-card-1">
          <div class="detail-icon">💒</div>
          <h3>Ceremony</h3>
          <p class="detail-time">4:00 PM</p>
          <p class="detail-location">St. Mary's Cathedral</p>
          <p class="detail-address">123 Church Street, Downtown</p>
        </div>

        <div class="detail-card detail-card-2">
          <div class="detail-icon">🥂</div>
          <h3>Reception</h3>
          <p class="detail-time">6:00 PM</p>
          <p class="detail-location">The Grand Ballroom</p>
          <p class="detail-address">456 Celebration Ave, Downtown</p>
        </div>

        <div class="detail-card detail-card-3">
          <div class="detail-icon">👔</div>
          <h3>Dress Code</h3>
          <p class="detail-time">Formal Attire</p>
          <p class="detail-info">Black tie optional</p>
          <p class="detail-note">We encourage elegant evening wear</p>
        </div>

        <div class="detail-card detail-card-4">
          <div class="detail-icon">🎁</div>
          <h3>Registry</h3>
          <p class="detail-time">Optional</p>
          <p class="detail-info">Your presence is the greatest gift</p>
          <p class="detail-note">Registry available at Amazon & Target</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingDetails'
}
</script>

<style scoped>
.wedding-details {
  padding: 5rem 0;
  background-color: #ffffff;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.intro-text {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
}

.decorative-line {
  width: 100px;
  height: 1px;
  background: linear-gradient(to right, transparent, #d4af37, transparent);
}

.section-title {
  font-family: 'Georgia', serif;
  font-size: 2.5rem;
  color: #2c3e50;
  text-align: center;
  font-weight: 300;
  margin: 0;
}

.invitation-text {
  text-align: center;
  max-width: 700px;
  margin: 2rem auto 4rem;
  font-size: 1.1rem;
  line-height: 1.8;
  color: #555;
  font-style: italic;
}

.details-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.detail-card {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: 2.5rem 2rem;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
  transition: transform 0.3s, box-shadow 0.3s;
  border: 1px solid rgba(212, 175, 55, 0.1);
}

/* Different transform effects for each card */
.detail-card-1:hover {
  transform: translateY(-10px) rotate(-2deg);
  box-shadow: 0 12px 35px rgba(212, 175, 55, 0.2);
}

.detail-card-2:hover {
  transform: translateY(-10px) rotate(2deg);
  box-shadow: 0 12px 35px rgba(212, 175, 55, 0.2);
}

.detail-card-3:hover {
  transform: translateY(-10px) scale(1.05);
  box-shadow: 0 12px 35px rgba(212, 175, 55, 0.2);
}

.detail-card-4:hover {
  transform: translateY(-15px);
  box-shadow: 0 15px 40px rgba(212, 175, 55, 0.25);
}

.detail-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.detail-card h3 {
  font-family: 'Georgia', serif;
  font-size: 1.5rem;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-weight: 400;
}

.detail-time {
  font-size: 1.2rem;
  color: #d4af37;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.detail-location {
  font-size: 1rem;
  color: #2c3e50;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.detail-address,
.detail-info,
.detail-note {
  font-size: 0.95rem;
  color: #666;
  line-height: 1.6;
  margin: 0.25rem 0;
}

@media (max-width: 768px) {
  .wedding-details {
    padding: 3rem 0;
  }

  .intro-text {
    flex-direction: column;
    gap: 1rem;
  }

  .decorative-line {
    width: 50px;
  }

  .section-title {
    font-size: 2rem;
  }

  .details-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .invitation-text {
    font-size: 1rem;
  }
}
</style>

