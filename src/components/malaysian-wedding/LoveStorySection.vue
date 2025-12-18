<template>
  <section class="love-story-section" ref="section">
    <div class="container">
      <!-- Title -->
      <h2 
        class="section-title"
        :class="{ 'fade-in-visible': isVisible }"
      >
        Our Love Story
      </h2>

      <!-- Photo with Decorations -->
      <div 
        class="photo-container"
        :class="{ 'fade-in-visible': isVisible }"
      >
        <div class="decorative-elements">
          <img class="decor decor-1" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_9_gxhtvn.png" alt="flower">
          <img class="decor decor-2" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_4_teposm.png" alt="flower">
          <img class="decor decor-number-1" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_2_edxq46.png" alt="number 1">
          <img class="decor decor-number-2" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_4_teposm.png" alt="number 2">
        </div>
        
        <div class="circular-frame">
          <img :src="storyPhoto" alt="Our Love Story" class="story-photo">
        </div>
      </div>

      <!-- Timeline -->
      <div class="timeline">
        <div 
          v-for="(event, index) in timeline" 
          :key="index"
          class="timeline-item"
          :class="{ 'slide-in': isVisible }"
          :style="{ transitionDelay: `${index * 0.2}s` }"
        >
          <h3 class="timeline-date">{{ event.date }}</h3>
          <p class="timeline-description">{{ event.description }}</p>
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
      isVisible: false,
      storyPhoto: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765906786/%EF%B8%8F_utuoqs.jpg',
      timeline: [
        {
          date: 'SEPTEMBER 2021',
          description: 'Awal Bertemu, lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Nulla facilisi cras fermentum odio eu feugiat pretium nibh ipsum.'
        },
        {
          date: 'SEPTEMBER 2022',
          description: 'Menjalin Hubungan, facilisis sed odio morbi quis commodo odio. Condimentum mattis pellentesque id nibh tortor id aliquet. Quis imperdiet massa tincidunt nunc pulvinar sapien et ligula ullamc orper. Vestibulum morbi blandit cursus risus.'
        },
        {
          date: 'SEPTEMBER 2023',
          description: 'Bertunangan, magna fermentum iaculis eu non. Pretium lectus quam id leo. Arcu vitae elementum curabitur vitae nunc sed.'
        },
        {
          date: 'SEPTEMBER 2024',
          description: 'Hari Pernikahan, Augue lacus viverra vitae congue eu consequat. Eget nunc scelerisque viverra mauris in aliquam sem fringilla.'
        }
      ]
    }
  },
  mounted() {
    window.addEventListener('scroll', this.checkVisibility)
    this.checkVisibility()
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.checkVisibility)
  },
  methods: {
    checkVisibility() {
      if (this.$refs.section) {
        const rect = this.$refs.section.getBoundingClientRect()
        this.isVisible = rect.top < window.innerHeight * 0.7
      }
    }
  }
}
</script>

<style scoped>
.love-story-section {
  padding: 4rem 1rem;
  background-color: #fbf3f0;
  position: relative;
  overflow: visible;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
}

/* Title */
.section-title {
  font-size: 5rem;
  font-family: 'Beloved Lovely', cursive;
  color: #2c2c2c;
  font-weight: 300;
  text-align: center;
  margin-bottom: 3rem;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.section-title.fade-in-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Photo Container */
.photo-container {
  position: relative;
  width: 100%;
  max-width: 500px;
  margin: 0 auto 4rem;
  opacity: 0;
  transform: scale(0.9);
  transition: all 0.8s ease-out 0.2s;
}

.photo-container.fade-in-visible {
  opacity: 1;
  transform: scale(1);
}

/* Decorative Elements */
.decorative-elements {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.decor {
  position: absolute;
  width: auto;
  height: auto;
}

.decor-1 {
  top: -10%;
  left: -20%;
  width: 180px;
}

.decor-2 {
  bottom: 10%;
  right: -15%;
  width: 200px;
  transform: rotate(15deg);
}

.decor-number-1 {
  top: 5%;
  left: -15%;
  width: 80px;
}

.decor-number-2 {
  top: 30%;
  right: -10%;
  width: 80px;
}

/* Circular Frame */
.circular-frame {
  width: 100%;
  aspect-ratio: 1;
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
  overflow: hidden;
  border: 3px solid rgba(212, 175, 55, 0.3);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
}

.story-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Timeline */
.timeline {
  position: relative;
  padding: 2rem 0;
}

.timeline-item {
  text-align: center;
  margin-bottom: 3rem;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease-out;
}

.timeline-item.slide-in {
  opacity: 1;
  transform: translateY(0);
}

.timeline-date {
  font-size: 1.1rem;
  font-weight: 600;
  letter-spacing: 2px;
  color: #2c2c2c;
  margin-bottom: 1rem;
  font-family: 'Montserrat', sans-serif;
}

.timeline-description {
  font-size: 1rem;
  line-height: 1.8;
  color: #2c2c2c;
  max-width: 600px;
  margin: 0 auto;
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 3.5rem;
    margin-bottom: 2rem;
  }

  .photo-container {
    max-width: 350px;
    margin-bottom: 3rem;
  }

  .decor-1 {
    width: 120px;
    left: -15%;
  }

  .decor-2 {
    width: 140px;
    right: -10%;
  }

  .decor-number-1,
  .decor-number-2 {
    width: 60px;
  }

  .timeline-date {
    font-size: 1rem;
  }

  .timeline-description {
    font-size: 0.95rem;
  }

  .timeline-item {
    margin-bottom: 2.5rem;
  }
}
</style>

