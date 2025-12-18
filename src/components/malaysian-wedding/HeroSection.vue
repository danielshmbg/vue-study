<template>
  <section class="hero-section">

    <!-- Main Content with Parallax -->
    <div 
      class="hero-content"
      :style="{ opacity: Math.max(0, 1 - scrollY / 1800) }"
    >
      <div class="flower-frame">
        <div 
          class="flower flower-tl">
          <img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714537/wedding_day_4_inh2i7.png" alt="Orn 1" style="width: 100%; height: 100%;">
        </div>
        <div class="flower flower-tr">
          <img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_7_yj5gts.png" alt="Orn 2" style="height: 90%; width: 90%;"></img></div>
        <div 
          class="flower flower-mid-left">
          <img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714535/hero_4_lkftnk.png" alt="Orn 3" style="width: 100%; height: 100%;"></img>
      </div>
      <div 
          class="flower flower-mid-right">
          <img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/hero_6_udusu6.png" alt="Orn 4" style="width: 100%; height: 100%;"></img>
      </div>
      <div 
          class="flower flower-bl">
          <img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714536/main_1_req3de.png" alt="Orn 5" style="width: 100%; height: 100%;"></img>
      </div>
        <div 
          class="flower flower-br"
          :style="{ transform: `rotate(${5 - scrollY * 0.03}deg) translateY(${scrollY * 0.05}px)` }"
        >🌺</div>
        
        <div class="couple-photo-placeholder" >
          <span class="photo-icon"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765714537/mobile_und_1_2_-_Copy_vrblhb.png" alt="Couple Photo" style="width: 100%; height: 100%;"></img></span>
        </div>
      </div>
      <div class="flower flower-bottom"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765847358/bride_groom_5_jxujpe.png" style="width: 70%; height: 70%;"></img></div>

      <div class="names-container">
        <div class="couple-names">
          <span class="name">{{ brideName }}</span>
          <span class="ampersand">&</span>
          <span class="name">{{ groomName }}</span>
        </div>
      </div>
      <div class="wedding-date-container">
        <div class="wedding-date">{{ weddingDate }}</div>
        <div class="wedding-subtitle">With heartfelt delight,
          <br>we invite you to witness our union </div>
        <div class="wedding-subtitle">“Two are better than one, because they have a good reward for their toil. For if they fall, one will lift up his fellow. But woe to him who is alone when he falls and has not another to lift him up.”
        <div class="wedding-subtitle">Ecclesiastes 4:9-10</div>
        </div>
      </div>
    
    
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  props: {
    scrollY: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      brideName: 'Cherina',
      groomName: 'Benhard',
      weddingDate: '15.03.2026'
    }
  }
}
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  padding: 4rem 1.5rem 4rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  position: relative;
  overflow: hidden;
  background-color: #fbf3f0;
}

.hero-decoration {
  position: absolute;
  inset: 0;
  pointer-events: none;
  height: 100svh;
}

.mountain-bg {
  position: absolute;
  bottom: 20%;
  left: 50%;
  transform: translateX(-50%);
  font-size: 10rem;
  opacity: 0.1;
  filter: blur(2px);
}

.trees {
  position: absolute;
  bottom: 10%;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-around;
  opacity: 0.15;
}

.tree {
  font-size: 4rem;
}

.clouds {
  position: absolute;
  top: 10%;
  left: 0;
  right: 0;
}

.cloud {
  position: absolute;
  font-size: 3rem;
  opacity: 0.2;
  animation: drift 20s linear infinite;
}

.cloud-1 {
  left: 10%;
  animation-delay: 0s;
}

.cloud-2 {
  left: 50%;
  animation-delay: 5s;
}

.cloud-3 {
  left: 80%;
  animation-delay: 10s;
}

@keyframes drift {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(calc(100vw + 100%));
  }
}

.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.flower-frame {
  position: relative;
  padding-top: 10%;
}

.flower {
  position: absolute;
  font-size: 2rem;
}

.flower-bottom {
  bottom: 0%;
  left: -24%;
}

.flower-tl {
  top: 10%;
  left: -8%;
  animation-delay: 0s;
  transform: scaleX(-1.27) scaleY(1.27);
}

.flower-tr {
  top: -8%;
  right: -10%;
  animation-delay: 0.5s;
  transform: rotate(-35deg) scaleX(0.8) scaleY(0.8);
}

.flower-mid-left {
  bottom: 18%;
  left: -15%;
  animation-delay: 1s;
  transform: rotate(-55deg) scaleX(0.7) scaleY(0.7);
}

.flower-mid-right {
  bottom: 18%;
  right: -15%;
  animation-delay: 1s;
  transform: rotate(-10deg) scaleX(0.7) scaleY(0.7);
}

.flower-bl {
  bottom: 10%;
  left: -24%;
  animation-delay: 1.5s;
  z-index: 2;
  transform: scaleX(0.9) scaleY(0.9);
}

.flower-br {
  bottom: 0;
  right: 0;
  animation-delay: 1.5s;
}

@keyframes sway {
  0%, 100% {
    transform: rotate(-5deg);
  }
  50% {
    transform: rotate(5deg);
  }
}

.couple-photo-placeholder {
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.couple-photo-placeholder::before {
  content: '';
  position: absolute;
  inset: -5px;
  border: 2px solid rgba(212, 175, 55, 0.2);
  border-radius: inherit;
}

.photo-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

.photo-icon img {
  display: block;
  max-width: 100%;
  height: auto;
}

.names-container {
  display: flex;
  margin-top: 2rem;
}

.couple-names {
  font-size: clamp(7rem, 10vw, 3.5rem);
  font-weight: 300;
  margin-bottom: 1rem;
  font-family: 'Beloved Lovely', cursive;
}

.name {
  display: inline-block;
  background-clip: text;
  color: black;
}

.ampersand {
  display: inline-block;
  margin: 0 1rem;
  color: black;
}

.wedding-date-container{
  display: flex;
  margin-left: 15%;
  margin-right: 15%;
  flex-direction: column;
}

.wedding-date {
  font-size: 1.6rem;
  color: #8b7355;
  letter-spacing: 3px;
  font-weight: 300;
  font-family: 'Montserrat', sans-serif;
}

.wedding-subtitle {
  font-family: 'Montserrat', sans-serif;
  font-size: 1.4rem;
  color: black;
  font-weight: 300;
  margin: 1rem 0;
}

.foreground-decoration {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  gap: 2rem;
  padding: 2rem;
  opacity: 0.4;
}

.grass, .flower-small {
  font-size: 2rem;
  animation: sway 4s ease-in-out infinite;
}

@media (max-width: 768px) {
  .couple-photo-placeholder {
    width: 420px;
  }

  .photo-icon {
    font-size: 4rem;
  }

  .flower {
    font-size: 2rem;
  }

  .wedding-date {
    font-size: 1.6rem;
    letter-spacing: 3px;
  }

  .mountain-bg {
    font-size: 10rem;
  }
}
</style>

