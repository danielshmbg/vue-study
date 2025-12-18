<template>
  <section class="wedding-gallery">
    <div class="container">
      <h2 class="section-title">Our Story</h2>
      <p class="section-subtitle">A glimpse into our journey together</p>

      <div class="gallery-grid">
        <div 
          v-for="(photo, index) in photos" 
          :key="index" 
          class="gallery-item"
          @click="openPhoto(index)"
        >
          <div class="photo-placeholder">
            <span class="photo-icon">{{ photo.icon }}</span>
            <div class="photo-overlay">
              <p class="photo-caption">{{ photo.caption }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hashtag-section">
        <h3>Share Your Photos</h3>
        <p>Use our wedding hashtag to share your favorite moments</p>
        <div class="hashtag">#EmilyAndJames2026</div>
        <p class="hashtag-note">We can't wait to see the day through your eyes!</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeddingGallery',
  data() {
    return {
      photos: [
        { icon: '💑', caption: 'First Meeting - 2020' },
        { icon: '🌹', caption: 'First Date' },
        { icon: '✈️', caption: 'Our First Trip Together' },
        { icon: '🎄', caption: 'First Christmas' },
        { icon: '🏔️', caption: 'Hiking Adventures' },
        { icon: '💍', caption: 'The Proposal' },
        { icon: '🎉', caption: 'Engagement Party' },
        { icon: '👗', caption: 'Dress Shopping' },
        { icon: '🥰', caption: 'Just Us' }
      ]
    }
  },
  methods: {
    openPhoto(index) {
      alert(`Photo ${index + 1}: ${this.photos[index].caption}\n\n(In production, this would open a photo viewer)`)
    }
  }
}
</script>

<style scoped>
.wedding-gallery {
  padding: 5rem 0;
  background: linear-gradient(to bottom, #f8f9fa 0%, #ffffff 100%);
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

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-bottom: 4rem;
}

.gallery-item {
  cursor: pointer;
  border-radius: 10px;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
}

.gallery-item:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
}

.photo-placeholder {
  position: relative;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  aspect-ratio: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.photo-icon {
  font-size: 5rem;
  filter: blur(2px);
  opacity: 0.5;
}

.photo-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  padding: 2rem 1rem 1rem;
  transform: translateY(100%);
  transition: transform 0.3s;
}

.gallery-item:hover .photo-overlay {
  transform: translateY(0);
}

.photo-caption {
  color: white;
  font-size: 1rem;
  text-align: center;
  margin: 0;
  font-weight: 600;
}

.hashtag-section {
  text-align: center;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: 3rem 2rem;
  border-radius: 15px;
  margin-top: 3rem;
}

.hashtag-section h3 {
  font-family: 'Georgia', serif;
  font-size: 2rem;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-weight: 300;
}

.hashtag-section p {
  color: #666;
  margin-bottom: 1.5rem;
  font-size: 1.05rem;
}

.hashtag {
  display: inline-block;
  background: linear-gradient(135deg, #d4af37, #f0e68c);
  color: #2c3e50;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1.8rem;
  font-weight: 700;
  margin: 1rem 0;
  box-shadow: 0 4px 15px rgba(212, 175, 55, 0.3);
  transition: transform 0.3s;
  cursor: pointer;
  font-family: monospace;
}

.hashtag:hover {
  transform: scale(1.05);
}

.hashtag-note {
  font-style: italic;
  color: #888;
  font-size: 0.95rem;
  margin-top: 1rem;
}

@media (max-width: 768px) {
  .wedding-gallery {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .gallery-grid {
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 1rem;
  }

  .photo-icon {
    font-size: 3rem;
  }

  .hashtag {
    font-size: 1.3rem;
    padding: 0.75rem 1.5rem;
  }

  .hashtag-section {
    padding: 2rem 1.5rem;
  }
}
</style>

