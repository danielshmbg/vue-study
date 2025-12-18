<template>
  <section class="content" id="about">
    <div class="container">
      <div class="content-grid">
        <div class="content-text">
          <h2>About This Project</h2>
          <p>
            This is a responsive Vue.js skeleton project built with modern web development practices.
            It provides a solid foundation for building your own Vue.js applications.
          </p>
          <p>
            The project uses Vue 3 with the Composition API, Vite for blazing-fast development,
            and follows responsive design principles to ensure your application looks great on
            all devices.
          </p>
          <ul class="features-list">
            <li>✅ Vue 3 with Composition API</li>
            <li>✅ Vite for fast development</li>
            <li>✅ Responsive design patterns</li>
            <li>✅ Modern CSS techniques</li>
            <li>✅ Component-based architecture</li>
          </ul>
        </div>
        <div class="content-image">
          <div class="placeholder-image">
            <span>📊</span>
            <p>Your content here</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Content'
}
</script>

<style scoped>
.content {
  padding: 4rem 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.content-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
}

.content-text h2 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
  color: #2c3e50;
}

.content-text p {
  margin-bottom: 1rem;
  line-height: 1.6;
  color: #666;
}

.features-list {
  list-style: none;
  padding: 0;
  margin-top: 1.5rem;
}

.features-list li {
  padding: 0.5rem 0;
  font-size: 1.1rem;
  color: #2c3e50;
}

.placeholder-image {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 8px;
  height: 400px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
}

.placeholder-image span {
  font-size: 4rem;
  margin-bottom: 1rem;
}

.placeholder-image p {
  font-size: 1.2rem;
  color: white;
}

/* Responsive styles */
@media (max-width: 968px) {
  .content-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .content-image {
    order: -1;
  }

  .placeholder-image {
    height: 300px;
  }
}

@media (max-width: 768px) {
  .content {
    padding: 3rem 0;
  }

  .content-text h2 {
    font-size: 1.5rem;
  }
}
</style>

