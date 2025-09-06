<template>
  <section class="hero" :class="{ 'loaded': isLoaded }">
    <!-- Interactive Background Layer -->
    <div class="hero-interactive-bg" ref="interactiveBg">
      <!-- Floating Buildings -->
      <div class="floating-buildings">
        <div class="building building-1" v-for="n in 8" :key="`building-${n}`" 
             :style="getBuildingStyle(n)">
          <div class="building-floors" :style="{ height: getRandomFloors(n) }">
            <div class="building-floor" v-for="floor in getFloorCount(n)" :key="floor"></div>
          </div>
          <div class="building-glow"></div>
        </div>
      </div>

      <!-- Animated Property Icons -->
      <div class="property-icons">
        <div class="property-icon" v-for="n in 15" :key="`icon-${n}`" 
             :style="getIconStyle(n)" @click="onIconClick(n)">
          <component :is="getPropertyIcon(n)" />
          <div class="icon-ripple"></div>
        </div>
      </div>

      <!-- Geometric Shapes -->
      <div class="geometric-shapes">
        <div class="shape" v-for="n in 20" :key="`shape-${n}`" 
             :style="getShapeStyle(n)" :class="`shape-${getShapeType(n)}`"></div>
      </div>

      <!-- Animated Network Lines -->
      <canvas ref="networkCanvas" class="network-canvas"></canvas>

      <!-- Market Data Animation -->
      <div class="market-data">
        <div class="data-point" v-for="n in 6" :key="`data-${n}`" 
             :style="getDataPointStyle(n)">
          <div class="data-value">{{ getMarketValue(n) }}</div>
          <div class="data-label">{{ getMarketLabel(n) }}</div>
          <div class="data-trend" :class="getTrendDirection(n)">
            <svg width="12" height="8" viewBox="0 0 12 8">
              <path d="M1 7L6 2L11 7" stroke="currentColor" stroke-width="2" fill="none"/>
            </svg>
          </div>
        </div>
      </div>
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
import { ref, onMounted, onUnmounted, inject } from 'vue'

// Property Icons Components
const HomeIcon = {
  template: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg>`
}

const BuildingIcon = {
  template: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M17 7l-1.41 1.41L18.17 11H8v2h10.17l-2.58 2.59L17 17l5-5-5-5zM4 5v14h4V5H4z"/></svg>`
}

const KeyIcon = {
  template: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12.65 10C11.83 7.67 9.61 6 7 6c-3.31 0-6 2.69-6 6s2.69 6 6 6c2.61 0 4.83-1.67 5.65-4H17v4h4v-4h2v-4H12.65zM7 14c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2z"/></svg>`
}

const TrendIcon = {
  template: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M16 6l2.29 2.29-4.88 4.88-4-4L2 16.59 3.41 18l6-6 4 4 6.3-6.29L22 12V6z"/></svg>`
}

const LocationIcon = {
  template: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/></svg>`
}

export default {
  name: 'HeroSection',
  components: {
    HomeIcon,
    BuildingIcon,
    KeyIcon,
    TrendIcon,
    LocationIcon
  },
  setup() {
    const openModal = inject('openModal')
    const isLoaded = ref(false)
    const interactiveBg = ref(null)
    const networkCanvas = ref(null)
    
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

    // Interactive Background Functions
    const getBuildingStyle = (index) => ({
      left: `${(index - 1) * 12 + Math.random() * 8}%`,
      bottom: `${Math.random() * 20}%`,
      animationDelay: `${index * 0.5}s`,
      animationDuration: `${8 + Math.random() * 4}s`
    })

    const getRandomFloors = (index) => `${60 + (index % 4) * 20 + Math.random() * 40}px`

    const getFloorCount = (index) => Math.floor(3 + (index % 6))

    const getIconStyle = (index) => ({
      left: `${Math.random() * 90 + 5}%`,
      top: `${Math.random() * 80 + 10}%`,
      animationDelay: `${index * 0.3}s`,
      animationDuration: `${6 + Math.random() * 4}s`
    })

    const getPropertyIcon = (index) => {
      const icons = ['HomeIcon', 'BuildingIcon', 'KeyIcon', 'TrendIcon', 'LocationIcon']
      return icons[index % icons.length]
    }

    const getShapeStyle = (index) => ({
      left: `${Math.random() * 100}%`,
      top: `${Math.random() * 100}%`,
      animationDelay: `${index * 0.2}s`,
      animationDuration: `${10 + Math.random() * 10}s`
    })

    const getShapeType = (index) => {
      const types = ['circle', 'square', 'triangle', 'diamond']
      return types[index % types.length]
    }

    const getDataPointStyle = (index) => ({
      left: `${85 + Math.random() * 10}%`,
      top: `${10 + index * 12}%`,
      animationDelay: `${index * 0.5}s`
    })

    const getMarketValue = (index) => {
      const values = ['₽2.4M', '↑15%', '€890K', '↗8.2%', '$1.1M', '↑12%']
      return values[index - 1] || '₽0'
    }

    const getMarketLabel = (index) => {
      const labels = ['Средняя цена', 'Рост за год', 'Премиум', 'Доходность', 'Элитное', 'Тренд']
      return labels[index - 1] || 'Данные'
    }

    const getTrendDirection = (index) => {
      return index % 2 === 0 ? 'trend-up' : 'trend-down'
    }

    const onIconClick = (index) => {
      // Add ripple effect and scale animation
      const icons = document.querySelectorAll('.property-icon')
      if (icons[index - 1]) {
        icons[index - 1].style.transform = 'scale(1.2)'
        setTimeout(() => {
          icons[index - 1].style.transform = 'scale(1)'
        }, 300)
      }
    }

    const initNetworkAnimation = () => {
      if (!networkCanvas.value) return
      
      const canvas = networkCanvas.value
      const ctx = canvas.getContext('2d')
      
      const resizeCanvas = () => {
        canvas.width = window.innerWidth
        canvas.height = window.innerHeight
      }
      
      resizeCanvas()
      window.addEventListener('resize', resizeCanvas)
      
      const nodes = []
      const nodeCount = 20
      
      for (let i = 0; i < nodeCount; i++) {
        nodes.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          vx: (Math.random() - 0.5) * 0.5,
          vy: (Math.random() - 0.5) * 0.5,
          radius: 2 + Math.random() * 3
        })
      }
      
      const animate = () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height)
        
        // Update nodes
        nodes.forEach(node => {
          node.x += node.vx
          node.y += node.vy
          
          if (node.x < 0 || node.x > canvas.width) node.vx *= -1
          if (node.y < 0 || node.y > canvas.height) node.vy *= -1
          
          // Draw node
          ctx.fillStyle = 'rgba(216, 4, 42, 0.6)'
          ctx.beginPath()
          ctx.arc(node.x, node.y, node.radius, 0, Math.PI * 2)
          ctx.fill()
        })
        
        // Draw connections
        ctx.strokeStyle = 'rgba(216, 4, 42, 0.2)'
        ctx.lineWidth = 1
        
        for (let i = 0; i < nodes.length; i++) {
          for (let j = i + 1; j < nodes.length; j++) {
            const dx = nodes[i].x - nodes[j].x
            const dy = nodes[i].y - nodes[j].y
            const distance = Math.sqrt(dx * dx + dy * dy)
            
            if (distance < 150) {
              ctx.beginPath()
              ctx.moveTo(nodes[i].x, nodes[i].y)
              ctx.lineTo(nodes[j].x, nodes[j].y)
              ctx.stroke()
            }
          }
        }
        
        requestAnimationFrame(animate)
      }
      
      animate()
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
      
      // Initialize network animation
      initNetworkAnimation()
    })
    
    return {
      openModal,
      isLoaded,
      interactiveBg,
      networkCanvas,
      heroStats,
      getParticleStyle,
      getBuildingStyle,
      getRandomFloors,
      getFloorCount,
      getIconStyle,
      getPropertyIcon,
      getShapeStyle,
      getShapeType,
      getDataPointStyle,
      getMarketValue,
      getMarketLabel,
      getTrendDirection,
      onIconClick,
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

.hero-video-layer iframe {
  width: 100%;
  height: 100%;
  object-fit: cover;
  pointer-events: none;
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

/* INTERACTIVE BACKGROUND ELEMENTS */
.hero-interactive-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 5;
  pointer-events: none;
  overflow: hidden;
}

/* Floating Buildings */
.floating-buildings {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 40%;
}

.building {
  position: absolute;
  bottom: 0;
  width: 60px;
  animation: buildingFloat infinite ease-in-out;
}

.building-floors {
  background: linear-gradient(180deg, rgba(216, 4, 42, 0.8) 0%, rgba(216, 4, 42, 0.6) 100%);
  width: 100%;
  position: relative;
  border-radius: 4px 4px 0 0;
  box-shadow: 0 0 20px rgba(216, 4, 42, 0.3);
}

.building-floor {
  height: 15px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  position: relative;
}

.building-floor:before {
  content: '';
  position: absolute;
  right: 5px;
  top: 3px;
  width: 8px;
  height: 8px;
  background: rgba(255, 255, 0, 0.8);
  border-radius: 1px;
  animation: windowBlink 3s infinite;
}

.building-glow {
  position: absolute;
  bottom: -10px;
  left: -20px;
  right: -20px;
  height: 20px;
  background: linear-gradient(180deg, transparent 0%, rgba(216, 4, 42, 0.4) 100%);
  border-radius: 50%;
  filter: blur(10px);
}

@keyframes buildingFloat {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-20px); }
}

@keyframes windowBlink {
  0%, 70% { opacity: 1; }
  85% { opacity: 0.3; }
  100% { opacity: 1; }
}

/* Property Icons */
.property-icons {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.property-icon {
  position: absolute;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(216, 4, 42, 0.9);
  border-radius: 50%;
  color: white;
  cursor: pointer;
  pointer-events: all;
  animation: iconFloat infinite ease-in-out;
  box-shadow: 0 4px 20px rgba(216, 4, 42, 0.4);
  transition: transform 0.3s ease;
}

.property-icon:hover {
  transform: scale(1.2);
  box-shadow: 0 6px 30px rgba(216, 4, 42, 0.6);
}

.icon-ripple {
  position: absolute;
  width: 60px;
  height: 60px;
  border: 2px solid rgba(216, 4, 42, 0.6);
  border-radius: 50%;
  animation: iconRipple 2s infinite;
}

@keyframes iconFloat {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  25% { transform: translateY(-10px) rotate(90deg); }
  50% { transform: translateY(0px) rotate(180deg); }
  75% { transform: translateY(-5px) rotate(270deg); }
}

@keyframes iconRipple {
  0% { transform: scale(0.8); opacity: 0.8; }
  50% { transform: scale(1.2); opacity: 0.4; }
  100% { transform: scale(1.6); opacity: 0; }
}

/* Geometric Shapes */
.geometric-shapes {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  opacity: 0.3;
  animation: shapeFloat infinite linear;
}

.shape-circle {
  border-radius: 50%;
  width: 20px;
  height: 20px;
  background: linear-gradient(45deg, rgba(216, 4, 42, 0.6), rgba(255, 255, 255, 0.3));
}

.shape-square {
  width: 15px;
  height: 15px;
  background: linear-gradient(45deg, rgba(216, 4, 42, 0.6), rgba(255, 255, 255, 0.3));
  transform: rotate(45deg);
}

.shape-triangle {
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 20px solid rgba(216, 4, 42, 0.6);
}

.shape-diamond {
  width: 16px;
  height: 16px;
  background: linear-gradient(45deg, rgba(216, 4, 42, 0.6), rgba(255, 255, 255, 0.3));
  transform: rotate(45deg);
  border-radius: 4px;
}

@keyframes shapeFloat {
  0% { transform: translateY(100vh) rotate(0deg); }
  100% { transform: translateY(-100px) rotate(360deg); }
}

/* Network Canvas */
.network-canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.6;
}

/* Market Data */
.market-data {
  position: absolute;
  top: 100px;
  right: 50px;
  z-index: 6;
  pointer-events: none;
}

.data-point {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  padding: 0.8rem 1.2rem;
  margin-bottom: 0.8rem;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  display: flex;
  align-items: center;
  gap: 0.8rem;
  animation: dataSlideIn 0.6s ease-out both;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.data-value {
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  font-size: 1.1rem;
}

.data-label {
  font-size: 0.8rem;
  opacity: 0.8;
  color: white;
}

.data-trend {
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.trend-up {
  color: #4CAF50;
}

.trend-down {
  color: #ff4444;
  transform: rotate(180deg);
}

@keyframes dataSlideIn {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
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
@media (max-width: 1024px) {
  /* Market Data Mobile Positioning */
  .market-data {
    right: 20px;
    top: 120px;
  }
  
  .data-point {
    padding: 0.6rem 1rem;
    margin-bottom: 0.6rem;
  }
  
  .data-value {
    font-size: 1rem;
  }
  
  .data-label {
    font-size: 0.7rem;
  }
}

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

  /* Interactive Background Mobile Adaptations */
  .floating-buildings {
    height: 30%;
  }
  
  .building {
    width: 40px;
  }
  
  .building-floors {
    border-radius: 2px 2px 0 0;
  }
  
  .building-floor {
    height: 12px;
  }
  
  .building-floor:before {
    width: 6px;
    height: 6px;
    right: 3px;
    top: 2px;
  }
  
  .property-icon {
    width: 32px;
    height: 32px;
  }
  
  .icon-ripple {
    width: 48px;
    height: 48px;
  }
  
  .shape-circle, .shape-square, .shape-diamond {
    width: 12px;
    height: 12px;
  }
  
  .shape-triangle {
    border-left-width: 6px;
    border-right-width: 6px;
    border-bottom-width: 12px;
  }
  
  /* Market Data Mobile */
  .market-data {
    display: none; /* Hide on mobile for cleaner look */
  }
  
  /* Network Canvas Mobile */
  .network-canvas {
    opacity: 0.3;
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
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }

  /* Further Mobile Optimizations for Interactive Background */
  .floating-buildings {
    height: 25%;
  }
  
  .building {
    width: 30px;
  }
  
  .building-floor {
    height: 10px;
  }
  
  .building-floor:before {
    width: 4px;
    height: 4px;
    right: 2px;
    top: 1px;
  }
  
  .property-icon {
    width: 28px;
    height: 28px;
  }
  
  .icon-ripple {
    width: 40px;
    height: 40px;
  }
  
  .shape {
    opacity: 0.2;
  }
  
  .shape-circle, .shape-square, .shape-diamond {
    width: 10px;
    height: 10px;
  }
  
  .shape-triangle {
    border-left-width: 5px;
    border-right-width: 5px;
    border-bottom-width: 10px;
  }
}

@media (max-width: 360px) {
  /* Ultra-small screens */
  .hero-interactive-bg {
    opacity: 0.7; /* Reduce overall intensity */
  }
  
  .floating-buildings {
    height: 20%;
  }
  
  .building {
    width: 25px;
  }
  
  .property-icon {
    width: 24px;
    height: 24px;
  }
  
  .icon-ripple {
    width: 36px;
    height: 36px;
  }
}
</style>