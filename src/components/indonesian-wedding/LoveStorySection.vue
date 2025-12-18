<template>
  <section class="love-story-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Our Love Story</h2>
        <div class="title-decoration">✨</div>
      </div>

      <div class="story-content">
        <div class="story-item" v-for="(chapter, index) in storyChapters" :key="index">
          <div class="story-icon">{{ chapter.icon }}</div>
          <div class="story-text">
            <h3 class="story-title">{{ chapter.title }}</h3>
            <p class="story-description">{{ chapter.description }}</p>
          </div>
        </div>
      </div>

      <div class="gallery-grid">
        <div 
          v-for="(photo, index) in photos" 
          :key="index" 
          class="gallery-item"
          :class="`gallery-item-${index + 1}`"
        >
          <div class="gallery-placeholder" :style="{ background: photo.gradient }">
            <span class="gallery-icon">{{ photo.icon }}</span>
            <div class="gallery-overlay">
              <p class="gallery-caption">{{ photo.caption }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'LoveStorySection',
  data() {
    return {
      storyChapters: [
        {
          icon: '🎯',
          title: 'First Meeting',
          description: 'We first met at a mutual friend\'s gathering in the spring of 2019. Little did we know that casual hello would change our lives forever.'
        },
        {
          icon: '☕',
          title: 'First Date',
          description: 'Three weeks later, Michael worked up the courage to ask Sarah for coffee. That coffee date turned into a five-hour conversation where time seemed to stand still.'
        },
        {
          icon: '✈️',
          title: 'Adventures Together',
          description: 'Over the next years, we explored the world together, creating countless memories from mountain hikes to beach sunsets. Each adventure brought us closer.'
        },
        {
          icon: '💍',
          title: 'The Proposal',
          description: 'On a beautiful autumn evening in 2024, during a sunset walk in our favorite park, Michael got down on one knee. Of course, Sarah said yes!'
        }
      ],
      photos: [
        { icon: '💑', caption: 'First Meeting - 2019', gradient: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)' },
        { icon: '🌹', caption: 'Our First Date', gradient: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)' },
        { icon: '🏔️', caption: 'Mountain Adventures', gradient: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)' },
        { icon: '🌅', caption: 'Beach Sunset', gradient: 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)' },
        { icon: '🎄', caption: 'First Christmas Together', gradient: 'linear-gradient(135deg, #30cfd0 0%, #330867 100%)' },
        { icon: '💍', caption: 'The Proposal', gradient: 'linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)' }
      ]
    }
  }
}
</script>

<style scoped>
.love-story-section {
  padding: 5rem 0;
  background: linear-gradient(to bottom, #ffffff 0%, #f8f9fa 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-family: 'Georgia', serif;
  font-size: clamp(2rem, 5vw, 3rem);
  color: #764ba2;
  margin-bottom: 0.5rem;
  font-weight: 400;
}

.title-decoration {
  font-size: 2rem;
}

.story-content {
  margin-bottom: 4rem;
}

.story-item {
  display: flex;
  gap: 2rem;
  margin-bottom: 3rem;
  align-items: flex-start;
  padding: 2rem;
  background: white;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s, box-shadow 0.3s;
}

.story-item:hover {
  transform: translateX(10px);
  box-shadow: 0 8px 30px rgba(118, 75, 162, 0.15);
}

.story-icon {
  font-size: 3rem;
  flex-shrink: 0;
}

.story-text {
  flex: 1;
}

.story-title {
  font-family: 'Georgia', serif;
  font-size: 1.5rem;
  color: #2c3e50;
  margin-bottom: 0.5rem;
  font-weight: 400;
}

.story-description {
  color: #666;
  line-height: 1.7;
  font-size: 1.05rem;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 3rem;
}

.gallery-item {
  border-radius: 15px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
}

.gallery-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.gallery-placeholder {
  position: relative;
  aspect-ratio: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.gallery-icon {
  font-size: 5rem;
  filter: blur(2px);
  opacity: 0.5;
}

.gallery-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  display: flex;
  align-items: flex-end;
  padding: 1.5rem;
  opacity: 0;
  transition: opacity 0.3s;
}

.gallery-item:hover .gallery-overlay {
  opacity: 1;
}

.gallery-caption {
  color: white;
  font-weight: 600;
  font-size: 1.05rem;
  margin: 0;
}

@media (max-width: 768px) {
  .love-story-section {
    padding: 3rem 0;
  }

  .story-item {
    flex-direction: column;
    gap: 1rem;
    padding: 1.5rem;
  }

  .story-item:hover {
    transform: translateY(-5px);
    transform: translateX(0);
  }

  .story-icon {
    font-size: 2.5rem;
  }

  .gallery-grid {
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 1rem;
  }

  .gallery-icon {
    font-size: 3rem;
  }
}
</style>

