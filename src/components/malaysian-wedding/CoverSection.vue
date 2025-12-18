<template>
  <section class="cover-section">
    <div class="cover-background">
      <div class="floating-elements">
        <div class="orn-top-left">
          <div class="leaf-static leaf-2"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_5_xb5vkj.png" alt="Leaf 2" style="width: 70%; height: 70%;"></img></div>
          <div class="leaf leaf-1"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707470/hero_8_qralcu.png" alt="Leaf 1" style="width: 40%; height: 40%;"></div>
          <div class="leaf-in leaf-3"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707470/hero_9_gxhtvn.png" alt="Leaf 3" style="width: 40%; height: 40%;"></img></div>
          <div class="bees bee-1"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707468/hero_1_tfrrxc.png" alt="Bee 1" style="width: 70%; height: 70%;"></img></div>
        </div>
        <div class="orn-top-right">
          <div class="leaf-static leaf-3a"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707470/hero_9_gxhtvn.png" alt="Leaf 3a" style="width: 40%; height: 40%;"></img></div>
          <div class="leaf-static leaf-4"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_6_zjckdm.png" alt="Leaf 4" style="width: 50%; height: 50%;"></img></div>
          <div class="leaf-static leaf-5"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707470/hero_7_nvi026.png" alt="Leaf 5" style="width: 70%; height: 70%;"></img></div>
        </div>
        <div class="orn-bottom-left">
          <div class="leaf-static leaf-6"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_3_zpwthr.png" alt="Leaf 2" style="width: 50%; height: 50%;"></img></div>
          <div class="leaf-static leaf-7"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_2_wlu7wi.png" alt="Leaf 1" style="width: 65%; height: 65%;"></div>
          <div class="leaf-static leaf-8"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707468/hero_4_vwmud9.png" alt="Leaf 3" style="width: 60%; height: 60%;"></img></div>
        </div>
        <div class="orn-bottom-right">
          <div class="leaf-static leaf-8a"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707468/hero_4_vwmud9.png" alt="Leaf 3a" style="width: 60%; height: 60%;"></img></div>
          <div class="leaf-static leaf-9"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_2_wlu7wi.png" alt="Leaf 4" style="width: 65%; height: 65%;"></img></div>
          <div class="leaf-static leaf-10"><img src="https://res.cloudinary.com/dfht26lv6/image/upload/v1765707469/hero_3_zpwthr.png" alt="Leaf 5" style="width: 60%; height: 60%;"></img></div>
        </div>
      </div>
    </div>

    <div class="cover-content">
      <p class="greeting-sub">The Wedding of</p>
      <div class="couple-names">
        <span class="name bride-name">{{ brideName }} & {{ groomName }}</span>
      </div>

      <p v-if="recipientName" class="recipient">
        Dear Mr./Mrs./Ms.<br />
        <span class="recipient-name">{{ recipientName }}</span>
      </p>

      <button class="open-btn" @click="$emit('open-invitation')">
        <span class="btn-text">Enter the Celebration</span>
      </button>
    </div>

  </section>
</template>

<script>
export default {
  name: 'CoverSection',
  props: {
    recipientName: {
      type: String,
      default: 'Bapak Sahala Sinurat dan Ibu'
    }
  },
  data() {
    return {
      brideName: 'Cherina',
      groomName: 'Benhard'
    }
  }
}
</script>

<style scoped>
.cover-section {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  background: linear-gradient(135deg, #fdfcfb 0%, #f5f0e8 50%, #ebe4d8 100%);
  overflow: hidden;
}

.cover-background {
  position: absolute;
  inset: 0;
  height: 100%;
  background-image: url('https://res.cloudinary.com/dfht26lv6/image/upload/v1765707470/hero_page_desktop_vmaklm.png');
  background-size: contain; /* show full image without cropping */
  background-position: center center;
  background-repeat: no-repeat;
  background-color: #f5f0e8; /* fallback color for empty areas */
}

.floating-elements {
  position: absolute;
  inset: 0;
}

.image-wrap {
  position: absolute;
}


img {
  width: 100%;
  height: auto;
}

.leaf {
  position: absolute;
  font-size: 1rem;
  animation: float 6s ease-in-out infinite;
  transform-origin: top center;
}

.leaf-static {
  position: absolute;
  font-size: 1rem;
}

.leaf-in {
  position: absolute;
  font-size: 1rem;
  animation: fadeIn 0.5sease-out;
}

.leaf-1 {
  top: -10%;
  left: 15%;
  animation-delay: 0s;
}

.bees {
  position: absolute;
  font-size: 1rem;
  animation: flying 3s ease-in-out infinite;
  transform-origin: center center;
}


.bee-1{
  top: 15%;
  left: 10%;
  animation-delay: 0s;
}

.leaf-2 {
  top: -17%;
  left: 0%;
  animation-delay: 1s;
}

.leaf-3 {
  top: -10%;
  left: 25%;
  animation-delay: 2s;
}

.leaf-3a {
  top: -10%;
  right: 20%;
  transform: scaleX(-1) rotate(-4deg);

}

.leaf-4 {
  top: -10%;
  right: 5%;
  animation-delay: 3s;
}

.leaf-5 {
  top: -15%;
  right: -5%;
  animation-delay: 4s;
}

.leaf-6 {
  bottom: 7%;
  left: -2%;
  animation-delay: 0s;
  transform: rotate(35deg);
}

.leaf-7 {
  bottom: -12%;
  left: 0%;
  transform:rotate(35deg);
}

.leaf-8 {
  bottom: -20%;
  left: 10%;
  animation-delay: 2s;
  transform:rotate(55deg);
}

.leaf-8a {
  bottom: -20%;
  right: 10%;
  transform: scaleX(-1) rotate(55deg);
}

.leaf-9 {
  bottom: -12%;
  right: 0%;
  animation-delay: 3s;
  transform: scaleX(-1) rotate(40deg);
}

.leaf-10 {
  bottom: 7%;
  right: -2%;
  animation-delay: 4s;
  transform: scaleX(-1) rotate(30deg);
}

@keyframes float {
  0%, 100% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-5px) rotate(5deg);
  }
}

@keyframes flying {
  0%, 100% {
    transform: translateY(0) rotate(0deg);
  }
 
  25% {
    transform: translateY(-10px) translateX(20px) rotate(5deg);
  }

  50% {
    transform: translateY(0px) rotate(5deg);
  }

  75% {
    transform: translateY(-10px) translateX(20px) ;
  }
}

.cover-content {
  position: absolute;
  bottom: 10vh; /* responsive vertical offset */
  left: 50%;
  transform: translateX(-50%);
  z-index: 1;
  text-align: center;
  width: 100%;
  max-width: 720px;
  padding: 0 2rem;
}

.cover-frame {
  position: relative;
  padding: 4rem 3rem;
  border: 2px solid rgba(212, 175, 55, 0.4);
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.08);
}

.ornament {
  position: absolute;
  font-size: 2rem;
  color: #d4af37;
  opacity: 0.6;
}

.top-left {
  top: 10px;
  left: 10px;
}

.top-right {
  top: 10px;
  right: 10px;
  transform: scaleX(-1);
}

.bottom-left {
  bottom: 10px;
  left: 10px;
  transform: scaleY(-1);
}

.bottom-right {
  bottom: 10px;
  right: 10px;
  transform: scale(-1);
}

.greeting {
  font-size: 1.5rem;
  color: #8b7355;
  margin-bottom: 0.5rem;
  font-style: italic;
  font-family: 'Montserrat', sans-serif;
}

.greeting-sub {
  font-size: 2rem;
  color: #f6f1ed;
  letter-spacing: -1px;
  margin-bottom: 1rem;
  font-weight: 100;
  font-family: 'Montserrat', sans-serif;
}

.couple-names {
  margin-bottom: 1rem;
}

.recipient {
  font-size: 1.2rem;
  color: #f6f1ed;
  margin-bottom: 1.5rem;
  line-height: 1.6;
  font-weight: 250;
  font-family: 'Montserrat', sans-serif;
}

.recipient-name {
  display: inline-block;
  margin-top: 0.3rem;
  letter-spacing: -0.5px;
  text-transform: capitalize;
  font-stretch: 200%;
}

.name {
  display: block;
  font-size: clamp(6rem, 10vw, 4.5rem);
  font-weight: 300;
  color: #f6f1ed;
  animation: fadeInUp 1s ease-out;
  font-family: 'Beloved Lovely', cursive;
  letter-spacing: 1px;
}

.bride-name {
  animation-delay: 0.2s;
  opacity: 0;
  animation-fill-mode: forwards;
}

.groom-name {
  animation-delay: 0.6s;
  opacity: 0;
  animation-fill-mode: forwards;
}

.ampersand {
  display: block;
  font-size: 2rem;
  color: #f6f1ed;
  margin: 0.5rem 0;
  font-family: 'Beloved Lovely', cursive;
}

.tagline {
  font-size: 1.3rem;
  color: #8b7355;
  margin-bottom: 2.5rem;
  font-style: italic;
}

.open-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2.5rem;
  background: linear-gradient(135deg, #7d8b6b, #7d8b6b);
  color: #f6f1ed;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 400;
  font-family: 'Montserrat', sans-serif;
  cursor: pointer;
  transition: all 0.3s;
  box-shadow: 0 10px 30px rgba(212, 175, 55, 0.25);
  animation: pulse 2s infinite;
}

.open-btn:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 15px 40px rgba(212, 175, 55, 0.4);
}

.btn-icon {
  font-size: 1.3rem;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0%, 100% {
    box-shadow: 0 10px 30px #7d8b6b77;
  }
  50% {
    box-shadow: 0 10px 40px #7d8b6b33;
  }
}

.scroll-hint {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  color: #a0917b;
  font-size: 0.9rem;
  animation: bounce 2s infinite;
}

.scroll-arrow {
  margin-top: 0.5rem;
  font-size: 1.5rem;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

@media (max-width: 768px) {
  .cover-content {
    bottom: 35%;
    padding: 0 1.5rem;
  }

  .greeting-sub {
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }

  .name {
    font-size: clamp(4rem, 10vw, 3.2rem);
    letter-spacing: 0.5px;
    line-height: 80%;
  }

  .recipient {
    font-size: 1rem;
  }

  .open-btn {
    padding: 0.85rem 2rem;
    font-size: 0.95rem;
  }

  .cover-background {
  position: absolute;
  inset: 0;
  height: 100%;
  background-image: url('https://res.cloudinary.com/dfht26lv6/image/upload/v1765720869/mobile_und_1_2_kpqrbb.png');
  background-size: auto; /* show full image without cropping */
  background-position: center center;
  background-repeat: no-repeat;
  background-color: #f5f0e8; /* fallback color for empty areas */
  }

.leaf-1 {
  top: -10%;
  left: 0%;
  animation-delay: 0s;
}

.leaf-2 {
  top: -17%;
  left: 5%;
  animation-delay: 1s;
}

.leaf-3 {
  top: -10%;
  left: 10%;
  animation-delay: 2s;
}

.leaf-3a {
  top: -10%;
  right: 10%;
  transform: scaleX(-1) rotate(-4deg);

}

.leaf-4 {
  top: -10%;
  right: 5%;
  animation-delay: 3s;
}

.leaf-5 {
  top: -15%;
  right: -20%;
  animation-delay: 4s;
}
}
</style>

