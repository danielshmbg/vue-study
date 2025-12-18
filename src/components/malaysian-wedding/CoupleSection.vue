<template>
  <section class="couple-section" ref="section">
    <div class="container">
      <!-- Bride -->
      <div 
        class="person-card bride-card"
        :class="{ 'fade-in-up': isVisible }"
      >
        <div class="decorative-elements bride-decor">
          <img class="decor decor-1" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_2_edxq46.png" alt="flower">
          <img class="decor decor-2" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847362/bride_groom_3_vazzzs.png" alt="flower">
          <img class="decor decor-2a" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_4_teposm.png" alt="flower">
          <img class="decor decor-2b" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_4_teposm.png" alt="flower">
          <img class="decor decor-3" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847359/bride_gorom_7_bugosv.png" alt="flower">
          <img class="decor decor-3a" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_3_zpwthr.png" alt="flower">
          <img class="decor decor-4" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_6_udusu6.png" alt="flower">
        </div>
        
        <div class="ornate-frame">
          <img class="frame-image" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847359/bride_groom1_err5nj.png" alt="frame">
          <div class="person-photo">
            <img :src="bridePhoto" alt="Bride" class="photo-img">
          </div>
        </div>

        <p class="person-title">THE BRIDE</p>
        <h3 class="person-name">{{ brideFullName }}</h3>
        <div class="parent-info">
          <p class="parent-label">Beloved daughter of {{ brideFather }}</p>
          <p class="parent-label">and {{ brideMother }}</p>
        </div>
        <button class="social-btn">@username</button>
      </div>

      <!-- Divider -->
      <div 
        class="couple-divider"
        :class="{ 'scale-in': isVisible }"
      >
        <span class="ampersand-large">&</span>
      </div>

      <!-- Groom -->
      <div 
        class="person-card groom-card"
        :class="{ 'fade-in-up': isVisible }"
      >
        <div class="decorative-elements groom-decor">
          <img class="decor decor-1" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_9_gxhtvn.png" alt="flower">
          <img class="decor decor-2" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_7_yj5gts.png" alt="flower">
          <img class="decor decor-3" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714535/hero_4_lkftnk.png" alt="flower">
          <img class="decor decor-4" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_6_udusu6.png" alt="flower">
        </div>
        
        <div class="ornate-frame">
          <img class="frame-image" src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847359/bride_groom1_err5nj.png" alt="frame">
          <div class="person-photo">
            <img :src="groomPhoto" alt="Groom" class="photo-img">
          </div>
        </div>

        <p class="person-title">THE GROOM</p>
        <h3 class="person-name">{{ groomFullName }}</h3>
        <div class="parent-info">
          <p class="parent-label">Cherished son of {{ groomFather }}</p>
          <p class="parent-label">and {{ groomMother }}</p>
        </div>
        <button class="social-btn">@username</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'CoupleSection',
  props: {
    scrollY: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      brideFullName: 'Cherina Widjaya',
      brideFather: 'Samuel Widjaya',
      brideMother: 'Helga Wiratman',
      bridePhoto: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765847360/bride_dptxal.png',
      groomFullName: 'Benhard William',
      groomFather: 'Ben Simajuntak',
      groomMother: 'Sonya Napitupulu',
      groomPhoto: 'https://res.cloudinary.com/dfht26lv6/image/upload/v1765847360/groom_ar0hfd.png',
      sectionTop: 0,
      isVisible: false
    }
  },
  computed: {
    parallaxOffset() {
      return Math.max(0, this.scrollY - this.sectionTop + 500)
    }
  },
  mounted() {
    this.updateSectionTop()
    window.addEventListener('resize', this.updateSectionTop)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.updateSectionTop)
  },
  watch: {
    scrollY() {
      this.checkVisibility()
    }
  },
  methods: {
    updateSectionTop() {
      if (this.$refs.section) {
        this.sectionTop = this.$refs.section.offsetTop
      }
    },
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
.couple-section {
  padding: 4rem 1rem;
  position: relative;
  overflow: hidden;
  background-color: #fbf3f0;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

/* Animation */
.person-card {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s ease-out;
}

.person-card.fade-in-up {
  opacity: 1;
  transform: translateY(0);
}

.couple-divider {
  opacity: 0;
  transform: scale(0.8);
  transition: all 0.6s ease-out 0.3s;
}

.couple-divider.scale-in {
  opacity: 1;
  transform: scale(1);
}

/* Person Card */
.person-card {
  text-align: center;
  padding: 2rem 1.5rem;
  position: relative;
}

/* Decorative Elements */
.decorative-elements {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.decor {
  position: absolute;
  width: 80px;
  height: auto;
  opacity: 1;
}

.bride-decor .decor-1 {
  top: 0%;
  left: -15%;
  width: 160px;
}

.bride-decor .decor-2 {
  top: -5%;
  right: -6%;
  width: 200px;
  transform: rotate(20deg)
}

.bride-decor .decor-2a {
  top: 18%;
  right: -15%;
  width: 190px;
  transform: rotate(35deg)
}

.bride-decor .decor-2b {
  top: 32%;
  left: -8%;
  width: 170px;
  transform: rotate(-50deg) scaleX(-1)
}

.bride-decor .decor-3 {
  bottom: 26%;
  left: -6%;
  width: 220px;
  transform: scaleX(-1) rotate(15deg)
}

.bride-decor .decor-3a {
  bottom: 32%;
  left: 0%;
  width: 160px;
  transform: rotate(-80deg);
}

.bride-decor .decor-4 {
  bottom: 35%;
  right: -5%;
  width: 55px;
}

.groom-decor .decor-1 {
  top: 5%;
  left: -5%;
  width: 60px;
  transform: scaleX(-1);
}

.groom-decor .decor-2 {
  top: 10%;
  right: 0%;
  width: 70px;
}

.groom-decor .decor-3 {
  bottom: 35%;
  left: -8%;
  width: 50px;
}

.groom-decor .decor-4 {
  bottom: 35%;
  right: -5%;
  width: 55px;
}

/* Ornate Frame */
.ornate-frame {
  position: relative;
  width: 500px;
  height: 650px;
  margin: 0 auto 1.5rem;
}

.frame-image {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
  z-index: 2;
  pointer-events: none;
}

.person-photo {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 87%;
  height: 80%;
  overflow: visible;
  border-radius: 50%;
  z-index: 1;
}

.photo-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Text Styles */
.person-title {
  font-size: 0.9rem;
  letter-spacing: 3px;
  color: #5c4a3d;
  margin-bottom: 0.5rem;
  font-weight: 600;
  font-family: 'Montserrat', sans-serif;
}

.person-name {
  font-size: 6rem;
  font-family: 'Beloved Lovely', cursive;
  color: #5c4a3d;
  font-weight: 300;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.parent-info {
  margin-bottom: 1.5rem;
}

.parent-label {
  font-size: 1rem;
  color: #5c4a3d;
  line-height: 1.6;
  margin: 0;
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
}

/* Social Button */
.social-btn {
  display: inline-flex;
  align-items: center;
  padding: 0.75rem 2rem;
  background: #6b8e6b;
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s;
  box-shadow: 0 4px 15px rgba(107, 142, 107, 0.3);
  font-family: 'Montserrat', sans-serif;
}

.social-btn:hover {
  background: #5a7a5a;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(107, 142, 107, 0.4);
}

/* Divider */
.couple-divider {
  text-align: center;
  padding: 2rem 0;
}

.ampersand-large {
  font-size: 4rem;
  font-family: 'Beloved Lovely', cursive;
  color: #5c4a3d;
  display: inline-block;
}

@media (max-width: 768px) {
  .ornate-frame {
    width: 240px;
    height: 300px;
  }

  .person-name {
    font-size: 2rem;
  }

  .decor {
    width: 60px;
  }

  .bride-decor .decor-1,
  .groom-decor .decor-1 {
    width: 50px;
  }

  .bride-decor .decor-2,
  .groom-decor .decor-2 {
    width: 60px;
  }

  .ampersand-large {
    font-size: 3rem;
  }
}
</style>

