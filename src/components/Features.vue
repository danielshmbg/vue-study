<template>
  <section class="features" id="features">
    <div class="container">
      <h2 class="section-title">Key Features</h2>
      <div class="features-grid">
        <div v-for="feature in features" :key="feature.id" class="feature-card">
          <div class="feature-icon">{{ feature.icon }}</div>
          <h3 class="feature-title">{{ feature.title }}</h3>
          <p class="feature-description">{{ feature.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Features',
  data() {
    return {
      features: [
        {
          id: 1,
          icon: '📱',
          title: 'Responsive Design',
          description: 'Fully responsive layout that works seamlessly on all devices and screen sizes.'
        },
        {
          id: 2,
          icon: '⚡',
          title: 'Fast & Modern',
          description: 'Built with Vite for lightning-fast development and optimized production builds.'
        },
        {
          id: 3,
          icon: '🎨',
          title: 'Clean UI',
          description: 'Beautiful and modern user interface with smooth animations and transitions.'
        },
        {
          id: 4,
          icon: '🔧',
          title: 'Easy to Customize',
          description: 'Well-organized code structure makes it easy to customize and extend.'
        },
        {
          id: 5,
          icon: '📦',
          title: 'Component-Based',
          description: 'Modular Vue components for better code reusability and maintainability.'
        },
        {
          id: 6,
          icon: '🚀',
          title: 'Production Ready',
          description: 'Optimized for production with best practices and performance in mind.'
        }
      ]
    }
  }
}
</script>

<style scoped>
.features {
  padding: 4rem 0;
  background-color: #f8f9fa;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.feature-card {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  text-align: center;
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature-title {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.feature-description {
  color: #666;
  line-height: 1.6;
}

/* Responsive styles */
@media (max-width: 768px) {
  .features {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .features-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
}
</style>

