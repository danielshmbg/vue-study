<template>
  <div class="audio-player" :class="{ playing: isPlaying }">
    <button class="audio-btn" @click="toggleAudio" :title="isPlaying ? 'Pause Music' : 'Play Music'">
      <span class="audio-icon">{{ isPlaying ? '🔊' : '🔇' }}</span>
      <span class="audio-waves" v-if="isPlaying">
        <span class="wave"></span>
        <span class="wave"></span>
        <span class="wave"></span>
      </span>
    </button>
    <span class="audio-label">{{ isPlaying ? 'Playing' : 'Tap to play' }}</span>
  </div>
</template>

<script>
export default {
  name: 'AudioPlayer',
  data() {
    return {
      isPlaying: false,
      audio: null
    }
  },
  methods: {
    toggleAudio() {
      this.isPlaying = !this.isPlaying
      // In production, this would control actual audio
      // this.audio.play() or this.audio.pause()
    }
  }
}
</script>

<style scoped>
.audio-player {
  position: fixed;
  top: 1.5rem;
  right: 1.5rem;
  z-index: 1000;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.5rem 1rem 0.5rem 0.5rem;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  border-radius: 50px;
  border: 1px solid rgba(212, 175, 55, 0.4);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  transition: all 0.3s;
}

.audio-player:hover {
  background: rgba(255, 255, 255, 1);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
}

.audio-player.playing {
  border-color: #d4af37;
}

.audio-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: linear-gradient(135deg, #d4af37, #f0d78c);
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s;
  position: relative;
}

.audio-btn:hover {
  transform: scale(1.1);
}

.audio-icon {
  font-size: 1.2rem;
}

.audio-waves {
  position: absolute;
  display: flex;
  gap: 2px;
  bottom: -8px;
}

.wave {
  width: 3px;
  height: 8px;
  background: #d4af37;
  border-radius: 2px;
  animation: wave 0.5s ease-in-out infinite;
}

.wave:nth-child(2) {
  animation-delay: 0.1s;
  height: 12px;
}

.wave:nth-child(3) {
  animation-delay: 0.2s;
}

@keyframes wave {
  0%, 100% {
    transform: scaleY(0.5);
  }
  50% {
    transform: scaleY(1);
  }
}

.audio-label {
  font-size: 0.85rem;
  color: #5c4a3d;
  white-space: nowrap;
}

@media (max-width: 768px) {
  .audio-player {
    top: 1rem;
    right: 1rem;
    padding: 0.4rem;
  }

  .audio-label {
    display: none;
  }

  .audio-btn {
    width: 36px;
    height: 36px;
  }
}
</style>

