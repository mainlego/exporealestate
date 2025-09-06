<template>
  <section class="hero" :class="{ 'loaded': isLoaded }">
    <!-- Background Video Layer -->
    <div class="hero-video-layer">
      <video autoplay muted loop playsinline @loadeddata="handleVideoLoaded" ref="heroVideo">
        <!-- Красивое видео Москва-Сити для демонстрации -->
        <source src="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4" type="video/mp4">
        <!-- Альтернативное видео -->
        <source src="https://sample-videos.com/zip/10/mp4/SampleVideo_1280x720_1mb.mp4" type="video/mp4">
      </video>
    </div>
    
    <!-- Background Image Layer (поверх видео) -->
    <div class="hero-image-layer">
      <div class="hero-background-image"></div>
    </div>
    
    <!-- Gradient Overlay -->
    <div class="hero-gradient-overlay"></div>
    
    <!-- Animated Particles -->
    <div class="particles-container">
      <div class="particle" v-for="n in 50" :key="n" :style="getParticleStyle(n)"></div>
    </div>
    
    <!-- Main Content -->
    <div class="hero-content">
      <div class="container">
        <div class="hero-text" :class="{ 'animate': isLoaded }">
          <div class="event-date" :style="{ animationDelay: '0.2s' }">
            <span class="date-icon">📅</span>
            Весна 2025, выставка недвижимости в Москве
          </div>
          
          <h1 :style="{ animationDelay: '0.4s' }">
            <span class="title-line">EXPO REAL</span>
            <span class="title-line highlight">ESTATE 2025</span>
          </h1>
          
          <p class="hero-subtitle" :style="{ animationDelay: '0.6s' }">
            Международная выставка недвижимости в Москве
          </p>
          
          <p class="hero-description" :style="{ animationDelay: '0.8s' }">
            EXPO REAL ESTATE — это важнейший международный хаб инвестиционной недвижимости, 
            который является мостом между крупнейшими российскими инвесторами и застройщиками со всего мира
          </p>
          
          <div class="hero-location interactive-card" :style="{ animationDelay: '1s' }" @mouseenter="handleLocationHover" @mouseleave="handleLocationLeave">
            <div class="location-icon">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none">
                <path d="M12 2C8.13 2 5 5.13 5 9C5 14.25 12 22 12 22S19 14.25 19 9C19 5.13 15.87 2 12 2ZM12 11.5C10.62 11.5 9.5 10.38 9.5 9S10.62 6.5 12 6.5S14.5 7.62 14.5 9S13.38 11.5 12 11.5Z" fill="currentColor"/>
              </svg>
              <div class="location-pulse"></div>
            </div>
            <div class="location-info">
              <strong>Деловой центр Москва-Сити</strong>
              <span>Пресненская набережная, 2</span>
              <div class="location-additional">🏢 Башня Федерация</div>
            </div>
          </div>
          
          <div class="hero-cta" :style="{ animationDelay: '1.2s' }">
            <h2>Станьте частью эксклюзивного<br>сообщества лидеров рынка<br>на EXPO REAL ESTATE</h2>
            <div class="cta-buttons">
              <button class="btn btn-primary btn-large" @click="openModal" @mouseenter="handleButtonHover">
                <span class="btn-text">Узнать подробнее</span>
                <span class="btn-icon">→</span>
              </button>
              <button class="btn btn-secondary btn-large" @click="scrollToStats">
                <span class="btn-text">Смотреть видео</span>
                <span class="btn-icon">▶</span>
              </button>
            </div>
          </div>
          
          <!-- Interactive Stats Preview -->
          <div class="hero-stats-preview" :style="{ animationDelay: '1.4s' }">
            <div class="stat-preview" v-for="stat in heroStats" :key="stat.id">
              <div class="stat-number">{{ stat.number }}</div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Enhanced Scroll Indicator -->
    <div class="scroll-indicator enhanced">
      <div class="scroll-text">Прокрутите вниз</div>
      <div class="scroll-mouse">
        <div class="scroll-wheel"></div>
      </div>
      <div class="scroll-arrows">
        <div class="scroll-arrow"></div>
        <div class="scroll-arrow"></div>
        <div class="scroll-arrow"></div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, onMounted, inject } from 'vue'

export default {
  name: 'HeroSection',
  setup() {
    const openModal = inject('openModal')
    const isLoaded = ref(false)
    const heroVideo = ref(null)
    
    const heroStats = ref([
      { id: 1, number: '15+', label: 'стран' },
      { id: 2, number: '500+', label: 'участников' },
      { id: 3, number: '30K+', label: 'посетителей' },
      { id: 4, number: '5.4B', label: '₽ объектов' }
    ])
    
    const getParticleStyle = (index) => {
      const randomX = Math.random() * 100
      const randomY = Math.random() * 100
      const randomSize = Math.random() * 4 + 1
      const randomDuration = Math.random() * 20 + 10
      const randomDelay = Math.random() * 5
      
      return {
        left: `${randomX}%`,
        top: `${randomY}%`,
        width: `${randomSize}px`,
        height: `${randomSize}px`,
        animationDuration: `${randomDuration}s`,
        animationDelay: `${randomDelay}s`
      }
    }
    
    const handleVideoLoaded = () => {
      setTimeout(() => {
        isLoaded.value = true
      }, 500)
    }
    
    const handleLocationHover = () => {
      // Можно добавить дополнительную анимацию при наведении
    }
    
    const handleLocationLeave = () => {
      // Можно добавить дополнительную анимацию при уходе курсора
    }
    
    const handleButtonHover = () => {
      // Можно добавить звуковые эффекты или дополнительные анимации
    }
    
    const scrollToStats = () => {
      const statsSection = document.querySelector('.stats')
      if (statsSection) {
        statsSection.scrollIntoView({ behavior: 'smooth' })
      }
    }
    
    onMounted(() => {
      // Запускаем анимацию загрузки через небольшую задержку
      setTimeout(() => {
        if (!isLoaded.value) {
          isLoaded.value = true
        }
      }, 2000)
    })
    
    return {
      openModal,
      isLoaded,
      heroVideo,
      heroStats,
      getParticleStyle,
      handleVideoLoaded,
      handleLocationHover,
      handleLocationLeave,
      handleButtonHover,
      scrollToStats
    }
  }
}
</script>

<style scoped>
/* HERO MAIN CONTAINER */
.hero {
  position: relative;
  height: 100vh;
  min-height: 700px;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  display: flex;
  align-items: center;
  overflow: hidden;
  background: #000;
}

.hero.loaded {
  animation: heroReveal 1s ease-out;
}

@keyframes heroReveal {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* BACKGROUND LAYERS */
.hero-video-layer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  opacity: 0.7;
}

.hero-video-layer video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-image-layer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 2;
  opacity: 0.3;
}

.hero-background-image {
  width: 100%;
  height: 100%;
  background-image: url('/assets/images/hero-background.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  mix-blend-mode: overlay;
}

.hero-gradient-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 3;
  background: linear-gradient(
    135deg,
    rgba(216, 4, 42, 0.1) 0%,
    rgba(0, 0, 0, 0.6) 30%,
    rgba(0, 0, 0, 0.4) 60%,
    rgba(216, 4, 42, 0.2) 100%
  );
}

/* PARTICLES ANIMATION */
.particles-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 4;
  pointer-events: none;
}

.particle {
  position: absolute;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  animation: float infinite linear;
  opacity: 0.6;
}

@keyframes float {
  0% {
    transform: translateY(100vh) rotate(0deg);
    opacity: 0;
  }
  10% {
    opacity: 0.6;
  }
  90% {
    opacity: 0.6;
  }
  100% {
    transform: translateY(-100px) rotate(360deg);
    opacity: 0;
  }
}

/* MAIN CONTENT */
.hero-content {
  position: relative;
  z-index: 10;
  width: 100%;
  padding-top: 80px;
}

.hero-text {
  color: white;
  max-width: 1000px;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.hero-text.animate {
  opacity: 1;
  transform: translateY(0);
}

/* EVENT DATE */
.event-date {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 2rem;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.9), rgba(216, 4, 42, 0.7));
  backdrop-filter: blur(15px);
  border-radius: 50px;
  font-size: 1rem;
  font-weight: var(--font-weight-medium);
  margin-bottom: 2rem;
  border: 1px solid rgba(216, 4, 42, 0.3);
  box-shadow: 0 8px 32px rgba(216, 4, 42, 0.3);
  animation: slideInDown 0.8s ease-out both;
}

.date-icon {
  font-size: 1.2rem;
}

/* TITLE */
.hero h1 {
  font-size: clamp(3.5rem, 8vw, 6rem);
  font-weight: var(--font-weight-bold);
  margin-bottom: 1.5rem;
  line-height: 0.9;
  animation: slideInUp 0.8s ease-out both;
}

.title-line {
  display: block;
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 3px 3px 8px rgba(0, 0, 0, 0.5);
}

.title-line.highlight {
  background: linear-gradient(135deg, #ff6b6b, #ff8e53, #ff6b9d);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  position: relative;
}

.title-line.highlight::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 0;
  width: 100px;
  height: 4px;
  background: linear-gradient(90deg, var(--color-primary), transparent);
  animation: lineExpand 1s ease-out 1.2s both;
}

@keyframes lineExpand {
  from { width: 0; }
  to { width: 200px; }
}

/* SUBTITLE & DESCRIPTION */
.hero-subtitle {
  font-size: 1.8rem;
  margin-bottom: 2rem;
  opacity: 0.95;
  font-weight: var(--font-weight-medium);
  animation: slideInUp 0.8s ease-out both;
}

.hero-description {
  font-size: 1.2rem;
  line-height: 1.8;
  margin-bottom: 3rem;
  opacity: 0.9;
  max-width: 800px;
  animation: slideInUp 0.8s ease-out both;
}

/* INTERACTIVE LOCATION CARD */
.hero-location {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  margin-bottom: 3rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  animation: slideInUp 0.8s ease-out both;
}

.hero-location:hover {
  transform: translateY(-5px);
  box-shadow: 0 16px 48px rgba(0, 0, 0, 0.4);
  background: rgba(255, 255, 255, 0.15);
}

.location-icon {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.location-icon svg {
  color: var(--color-primary);
  filter: drop-shadow(0 0 10px rgba(216, 4, 42, 0.5));
  z-index: 1;
}

.location-pulse {
  position: absolute;
  width: 40px;
  height: 40px;
  border: 2px solid var(--color-primary);
  border-radius: 50%;
  opacity: 0.6;
  animation: locationPulse 2s infinite;
}

@keyframes locationPulse {
  0% {
    transform: scale(0.8);
    opacity: 0.8;
  }
  50% {
    transform: scale(1.2);
    opacity: 0.3;
  }
  100% {
    transform: scale(1.6);
    opacity: 0;
  }
}

.location-info strong {
  display: block;
  font-size: 1.3rem;
  margin-bottom: 0.5rem;
  color: white;
}

.location-info span {
  display: block;
  opacity: 0.9;
  font-size: 1rem;
  margin-bottom: 0.25rem;
}

.location-additional {
  font-size: 0.9rem;
  opacity: 0.7;
  color: var(--color-primary);
}

/* CTA SECTION */
.hero-cta h2 {
  font-size: clamp(2rem, 4.5vw, 3rem);
  margin-bottom: 3rem;
  line-height: 1.3;
  font-weight: var(--font-weight-semibold);
  animation: slideInUp 0.8s ease-out both;
}

.cta-buttons {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 3rem;
  animation: slideInUp 0.8s ease-out both;
}

.btn-large {
  position: relative;
  padding: 1.5rem 3rem;
  font-size: 1.1rem;
  font-weight: var(--font-weight-semibold);
  border-radius: 60px;
  display: flex;
  align-items: center;
  gap: 1rem;
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.btn-primary {
  background: linear-gradient(135deg, var(--color-primary), #ff1744);
  box-shadow: 0 8px 32px rgba(216, 4, 42, 0.4);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 8px 32px rgba(255, 255, 255, 0.1);
}

.btn-large:hover {
  transform: translateY(-3px) scale(1.05);
}

.btn-primary:hover {
  box-shadow: 0 16px 48px rgba(216, 4, 42, 0.6);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.2);
  box-shadow: 0 16px 48px rgba(255, 255, 255, 0.2);
}

.btn-icon {
  font-size: 1.3rem;
  transition: transform 0.3s ease;
}

.btn-large:hover .btn-icon {
  transform: translateX(5px);
}

/* HERO STATS PREVIEW */
.hero-stats-preview {
  display: flex;
  gap: 2rem;
  animation: slideInUp 0.8s ease-out both;
}

.stat-preview {
  text-align: center;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
}

.stat-preview:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-5px);
}

.stat-number {
  font-size: 1.5rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.9rem;
  opacity: 0.8;
}

/* ENHANCED SCROLL INDICATOR */
.scroll-indicator.enhanced {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  color: white;
  z-index: 10;
  opacity: 0.8;
}

.scroll-text {
  font-size: 0.9rem;
  margin-bottom: 1rem;
  opacity: 0.7;
}

.scroll-mouse {
  width: 24px;
  height: 40px;
  border: 2px solid rgba(255, 255, 255, 0.5);
  border-radius: 12px;
  margin: 0 auto 1rem;
  position: relative;
}

.scroll-wheel {
  width: 4px;
  height: 8px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 2px;
  position: absolute;
  top: 8px;
  left: 50%;
  transform: translateX(-50%);
  animation: scrollWheel 2s infinite;
}

@keyframes scrollWheel {
  0%, 20% {
    transform: translateX(-50%) translateY(0);
    opacity: 1;
  }
  100% {
    transform: translateX(-50%) translateY(16px);
    opacity: 0;
  }
}

.scroll-arrows {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.scroll-arrow {
  width: 20px;
  height: 20px;
  border-right: 2px solid rgba(255, 255, 255, 0.4);
  border-bottom: 2px solid rgba(255, 255, 255, 0.4);
  transform: rotate(45deg);
  margin: 0 auto;
  animation: scrollArrow 2s infinite;
}

.scroll-arrow:nth-child(2) { animation-delay: 0.2s; }
.scroll-arrow:nth-child(3) { animation-delay: 0.4s; }

@keyframes scrollArrow {
  0%, 20% {
    opacity: 1;
    transform: rotate(45deg) translateY(0);
  }
  100% {
    opacity: 0;
    transform: rotate(45deg) translateY(10px);
  }
}

/* ANIMATION KEYFRAMES */
@keyframes slideInDown {
  from {
    opacity: 0;
    transform: translateY(-50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* RESPONSIVE DESIGN */
@media (max-width: 768px) {
  .hero {
    min-height: 600px;
  }
  
  .hero-text {
    text-align: center;
  }
  
  .hero-location {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
    padding: 1.5rem;
  }
  
  .cta-buttons {
    flex-direction: column;
    gap: 1rem;
  }
  
  .hero-stats-preview {
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: center;
  }
  
  .stat-preview {
    min-width: 120px;
  }
  
  .btn-large {
    padding: 1.25rem 2rem;
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .hero-content {
    padding-top: 60px;
  }
  
  .event-date {
    font-size: 0.9rem;
    padding: 0.6rem 1.5rem;
  }
  
  .hero-description {
    font-size: 1rem;
  }
  
  .hero-stats-preview {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>