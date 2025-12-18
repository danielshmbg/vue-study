<template>
  <div id="app">
    <!-- Multi-page selector -->
    <div v-if="currentPage === 'landing'">
      <Header />
      <main class="main-content">
        <Hero />
        <Features />
        <Content />
      </main>
      <Footer />
    </div>
    <div v-else-if="currentPage === 'elegant-wedding'">
      <WeddingInvitation />
    </div>
    <div v-else-if="currentPage === 'indonesian-wedding'">
      <IndonesianWedding />
    </div>
    <div v-else-if="currentPage === 'malaysian-wedding'">
      <MalaysianWedding />
    </div>

    <!-- Page Toggle Menu -->
    <div class="page-menu" :class="{ open: menuOpen }">
      <button class="menu-toggle" @click="menuOpen = !menuOpen">
        <span v-if="!menuOpen">📄 Pages</span>
        <span v-else>✕ Close</span>
      </button>
      
      <div v-if="menuOpen" class="menu-options">
        <button 
          @click="changePage('landing')" 
          class="menu-option"
          :class="{ active: currentPage === 'landing' }"
        >
          🏠 Landing Page
        </button>
        <button 
          @click="changePage('elegant-wedding')" 
          class="menu-option"
          :class="{ active: currentPage === 'elegant-wedding' }"
        >
          💒 Elegant Wedding
        </button>
        <button 
          @click="changePage('indonesian-wedding')" 
          class="menu-option"
          :class="{ active: currentPage === 'indonesian-wedding' }"
        >
          🎉 Modern Wedding
        </button>
        <button 
          @click="changePage('malaysian-wedding')" 
          class="menu-option"
          :class="{ active: currentPage === 'malaysian-wedding' }"
        >
          ✨ Romantic Dark
        </button>
      </div>
    </div>
  </div>
</template>

<script>
// Landing Page Components
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Features from './components/Features.vue'
import Content from './components/Content.vue'
import Footer from './components/Footer.vue'

// Wedding Invitation Components
import WeddingInvitation from './components/wedding/WeddingInvitation.vue'
import IndonesianWedding from './components/indonesian-wedding/IndonesianWedding.vue'
import MalaysianWedding from './components/malaysian-wedding/MalaysianWedding.vue'

export default {
  name: 'App',
  components: {
    Header,
    Hero,
    Features,
    Content,
    Footer,
    WeddingInvitation,
    IndonesianWedding,
    MalaysianWedding
  },
  data() {
    return {
      currentPage: 'malaysian-wedding', // Default to the new malaysian wedding template
      menuOpen: false
    }
  },
  methods: {
    changePage(page) {
      this.currentPage = page
      this.menuOpen = false
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }
  }
}
</script>

<style scoped>
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
}

.page-menu {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  z-index: 9999;
}

.menu-toggle {
  padding: 0.75rem 1.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  transition: all 0.3s;
  white-space: nowrap;
}

.menu-toggle:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(118, 75, 162, 0.4);
}

.menu-options {
  position: absolute;
  bottom: 100%;
  right: 0;
  margin-bottom: 1rem;
  background: white;
  border-radius: 15px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  padding: 0.5rem;
  min-width: 200px;
  animation: slideUp 0.3s ease-out;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.menu-option {
  display: block;
  width: 100%;
  padding: 0.75rem 1rem;
  background: transparent;
  color: #2c3e50;
  border: none;
  border-radius: 10px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
  text-align: left;
  margin-bottom: 0.25rem;
}

.menu-option:hover {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  transform: translateX(-3px);
}

.menu-option.active {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  color: white;
}

.menu-option:last-child {
  margin-bottom: 0;
}

@media (max-width: 768px) {
  .page-menu {
    bottom: 1rem;
    right: 1rem;
  }

  .menu-toggle {
    padding: 0.6rem 1.2rem;
    font-size: 0.9rem;
  }

  .menu-options {
    min-width: 180px;
  }

  .menu-option {
    padding: 0.6rem 0.75rem;
    font-size: 0.85rem;
  }
}
</style>


