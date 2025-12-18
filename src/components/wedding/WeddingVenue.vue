<template>
  <section class="wedding-venue">
    <div class="container">
      <h2 class="section-title">Location & Directions</h2>
      <p class="section-subtitle">Find your way to our celebration</p>

      <div class="venue-grid">
        <div class="venue-card">
          <div class="venue-header">
            <div class="venue-icon">💒</div>
            <h3>Ceremony Venue</h3>
          </div>
          <div class="venue-details">
            <h4>St. Mary's Cathedral</h4>
            <p class="venue-address">
              <span class="address-icon">📍</span>
              123 Church Street<br>
              Downtown, State 12345
            </p>
            <div class="venue-info">
              <p><strong>Parking:</strong> Available on-site and street parking</p>
              <p><strong>Accessibility:</strong> Wheelchair accessible</p>
            </div>
            <button class="map-button" @click="openMap('ceremony')">
              View on Map 🗺️
            </button>
          </div>
        </div>

        <div class="venue-card">
          <div class="venue-header">
            <div class="venue-icon">🥂</div>
            <h3>Reception Venue</h3>
          </div>
          <div class="venue-details">
            <h4>The Grand Ballroom</h4>
            <p class="venue-address">
              <span class="address-icon">📍</span>
              456 Celebration Avenue<br>
              Downtown, State 12345
            </p>
            <div class="venue-info">
              <p><strong>Parking:</strong> Valet service available</p>
              <p><strong>Accessibility:</strong> Wheelchair accessible</p>
            </div>
            <button class="map-button" @click="openMap('reception')">
              View on Map 🗺️
            </button>
          </div>
        </div>
      </div>

      <div class="accommodation-section">
        <h3 class="accommodation-title">Accommodation</h3>
        <p class="accommodation-text">
          For out-of-town guests, we have reserved room blocks at the following hotels:
        </p>
        <div class="hotel-list">
          <div class="hotel-item">
            <h4>🏨 The Grand Hotel</h4>
            <p>Just 5 minutes from venues</p>
            <p>Use code: <strong>EMILY-JAMES</strong></p>
          </div>
          <div class="hotel-item">
            <h4>🏨 Comfort Suites</h4>
            <p>10 minutes from venues</p>
            <p>Use code: <strong>EMILY-JAMES</strong></p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingVenue',
  methods: {
    openMap(venue) {
      // In a real application, this would open Google Maps with the actual address
      const addresses = {
        ceremony: '123 Church Street, Downtown',
        reception: '456 Celebration Avenue, Downtown'
      }
      alert(`Opening map for: ${addresses[venue]}\n\n(In production, this would open Google Maps)`)
    }
  }
}
</script>

<style scoped>
.wedding-venue {
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
  color: #666;
  font-size: 1.1rem;
  margin-bottom: 3rem;
  font-style: italic;
}

.venue-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.venue-card {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
  transition: transform 0.3s, box-shadow 0.3s;
}

.venue-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 30px rgba(212, 175, 55, 0.15);
}

.venue-header {
  background: linear-gradient(135deg, #d4af37, #f0e68c);
  padding: 2rem;
  text-align: center;
}

.venue-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.venue-header h3 {
  font-family: 'Georgia', serif;
  font-size: 1.8rem;
  color: #2c3e50;
  margin: 0;
  font-weight: 400;
}

.venue-details {
  padding: 2rem;
}

.venue-details h4 {
  font-size: 1.5rem;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-weight: 600;
}

.venue-address {
  color: #555;
  line-height: 1.8;
  margin-bottom: 1.5rem;
  font-size: 1.05rem;
}

.address-icon {
  font-size: 1.2rem;
  margin-right: 0.5rem;
}

.venue-info {
  background: rgba(212, 175, 55, 0.1);
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1.5rem;
}

.venue-info p {
  margin: 0.5rem 0;
  color: #666;
  font-size: 0.95rem;
}

.venue-info strong {
  color: #2c3e50;
}

.map-button {
  width: 100%;
  padding: 0.75rem;
  background: linear-gradient(135deg, #d4af37, #f0e68c);
  color: #2c3e50;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
}

.map-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
}

.accommodation-section {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: 3rem;
  border-radius: 15px;
  text-align: center;
}

.accommodation-title {
  font-family: 'Georgia', serif;
  font-size: 2rem;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-weight: 300;
}

.accommodation-text {
  color: #666;
  margin-bottom: 2rem;
  font-size: 1.05rem;
}

.hotel-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.hotel-item {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
}

.hotel-item h4 {
  color: #2c3e50;
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
}

.hotel-item p {
  color: #666;
  margin: 0.25rem 0;
  font-size: 0.95rem;
}

.hotel-item strong {
  color: #d4af37;
  font-size: 1.1rem;
}

@media (max-width: 768px) {
  .wedding-venue {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .venue-grid {
    grid-template-columns: 1fr;
  }

  .accommodation-section {
    padding: 2rem 1.5rem;
  }

  .hotel-list {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
</style>

