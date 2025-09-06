<template>
  <section class="geography section full-width" ref="geographySection">
    <!-- Interactive Background -->
    <div class="geography-background">
      <div class="world-grid"></div>
      <div class="floating-continents">
        <div class="continent" v-for="n in 6" :key="n" :style="getContinentStyle(n)"></div>
      </div>
      <div class="connection-lines">
        <svg class="connections-svg" width="100%" height="100%">
          <defs>
            <linearGradient id="connectionGradient" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="rgba(216, 4, 42, 0.8)" />
              <stop offset="100%" stop-color="rgba(216, 4, 42, 0.2)" />
            </linearGradient>
          </defs>
          <path 
            v-for="(line, index) in connectionPaths" 
            :key="index" 
            :d="line" 
            stroke="url(#connectionGradient)" 
            stroke-width="2" 
            fill="none"
            :style="{ animationDelay: `${index * 0.5}s` }"
            class="connection-path"
          />
        </svg>
      </div>
    </div>
    
    <div class="container">
        <div class="geography-header text-center" :class="{ 'animate': isVisible }">
        <div class="header-badge">
          <span class="badge-icon">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12,2C6.47,2 2,6.47 2,12C2,17.53 6.47,22 12,22C17.53,22 22,17.53 22,12C22,6.47 17.53,2 12,2M15.59,7L12,10.59L8.41,7L7,8.41L10.59,12L7,15.59L8.41,17L12,13.41L15.59,17L17,15.59L13.41,12L17,8.41L15.59,7Z"/>
            </svg>
          </span>
          Мировое присутствие
        </div>
        <h2>География участников</h2>
        <p class="section-subtitle">
          Expo Real Estate собирает в одном месте проверенных застройщиков из более чем 15 стран мира
        </p>
      </div>
      
      <div class="geography-content" :class="{ 'animate': isVisible }">
        <div class="geography-text">
          <div class="text-content">
            <h3>Международные партнеры</h3>
            <p>
              Уникальная возможность изучить лучшие варианты для инвестирования 
              и получить выгодные предложения от проверенных партнеров.
            </p>
            <div class="geography-stats">
              <div class="stat-item" v-for="stat in geographyStats" :key="stat.id">
                <span class="stat-icon" v-html="stat.icon"></span>
                <div class="stat-content">
                  <span class="stat-number">{{ stat.value }}</span>
                  <span class="stat-label">{{ stat.label }}</span>
                </div>
              </div>
            </div>
            <div class="action-buttons">
              <button class="btn btn-primary btn-large" @click="openModal">
                <span>Узнать больше</span>
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M8.59,16.58L13.17,12L8.59,7.41L10,6L16,12L10,18L8.59,16.58Z"/>
                </svg>
              </button>
              <button class="btn btn-secondary btn-large" @click="showInteractiveMap">
                <span>Интерактивная карта</span>
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M15,19L9,16.89V5L15,7.11M20.5,3C20.44,3 20.39,3 20.34,3L15,5.1L9,3L3.36,4.9C3.15,4.97 3,5.15 3,5.38V20.5A0.5,0.5 0 0,0 3.5,21C3.55,21 3.61,21 3.66,20.97L9,18.9L15,21L20.64,19.1C20.85,19.03 21,18.85 21,18.62V3.5A0.5,0.5 0 0,0 20.5,3Z"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
        
        <div class="geography-visual">
          <div class="interactive-world-map" :class="{ 'map-active': isMapInteractive }">
            <div class="map-container">
              <img src="/assets/images/karta.jpg" alt="География участников" />
              <div class="map-overlay"></div>
              <div class="map-points">
                <div 
                  class="enhanced-point" 
                  v-for="(point, index) in mapPoints" 
                  :key="point.id"
                  :class="`point-${point.id}`"
                  :style="{ animationDelay: `${index * 0.2}s` }"
                  @click="selectCountry(point)"
                  @mouseenter="showCountryInfo(point)"
                  @mouseleave="hideCountryInfo"
                >
                  <div class="point-pulse"></div>
                  <div class="point-core"></div>
                  <div class="point-tooltip">{{ point.country }}</div>
                </div>
              </div>
            </div>
            
            <div class="map-legend">
              <h4>Легенда карты</h4>
              <div class="legend-items">
                <div class="legend-item">
                  <div class="legend-dot active"></div>
                  <span>Активные страны (участники)</span>
                </div>
                <div class="legend-item">
                  <div class="legend-dot potential"></div>
                  <span>Потенциальные партнеры</span>
                </div>
              </div>
            </div>
          </div>
          
          <div class="countries-showcase">
            <div class="showcase-header">
              <h4>Страны-участники</h4>
              <div class="showcase-counter">{{ countries.length }} стран</div>
            </div>
            <div class="countries-grid">
              <div 
                class="country-card" 
                v-for="(country, index) in countries" 
                :key="country"
                :class="{ 'active': selectedCountry === country }"
                :style="{ animationDelay: `${index * 0.05}s` }"
                @click="selectCountry({ country })"
              >
                <div class="country-flag">🌍</div>
                <span class="country-name">{{ country }}</span>
                <div class="country-indicator"></div>
              </div>
            </div>
            <div class="showcase-stats">
              <div class="showcase-stat">
                <span class="stat-number">15+</span>
                <span class="stat-text">Стран</span>
              </div>
              <div class="showcase-stat">
                <span class="stat-number">500+</span>
                <span class="stat-text">Компаний</span>
              </div>
              <div class="showcase-stat">
                <span class="stat-number">10K+</span>
                <span class="stat-text">Объектов</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, onMounted, onUnmounted, inject } from 'vue'

export default {
  name: 'GeographySection',
  setup() {
    const openModal = inject('openModal')
    const geographySection = ref(null)
    const isVisible = ref(false)
    const isMapInteractive = ref(false)
    const selectedCountry = ref(null)
    
    const geographyStats = ref([
      {
        id: 1,
        value: '15+',
        label: 'Стран мира',
        icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12,2C6.47,2 2,6.47 2,12C2,17.53 6.47,22 12,22C17.53,22 22,17.53 22,12C22,6.47 17.53,2 12,2M15.59,7L12,10.59L8.41,7L7,8.41L10.59,12L7,15.59L8.41,17L12,13.41L15.59,17L17,15.59L13.41,12L17,8.41L15.59,7Z"/></svg>`
      },
      {
        id: 2,
        value: '500+',
        label: 'Компаний',
        icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12,5.5A3.5,3.5 0 0,1 15.5,9A3.5,3.5 0 0,1 12,12.5A3.5,3.5 0 0,1 8.5,9A3.5,3.5 0 0,1 12,5.5M5,8C5.56,8 6.08,8.15 6.53,8.42C6.38,9.85 6.8,11.27 7.66,12.38C7.16,13.34 6.16,14 5,14A3,3 0 0,1 2,11A3,3 0 0,1 5,8M19,8A3,3 0 0,1 22,11A3,3 0 0,1 19,14C17.84,14 16.84,13.34 16.34,12.38C17.2,11.27 17.62,9.85 17.47,8.42C17.92,8.15 18.44,8 19,8M5.5,18.25C5.5,16.18 8.41,14.5 12,14.5C15.59,14.5 18.5,16.18 18.5,18.25V20H5.5V18.25M0,20V18.5C0,17.11 1.89,15.94 4.45,15.6C3.86,16.28 3.5,17.22 3.5,18.25V20H0M24,20H20.5V18.25C20.5,17.22 20.14,16.28 19.55,15.6C22.11,15.94 24,17.11 24,18.5V20Z"/></svg>`
      },
      {
        id: 3,
        value: '10K+',
        label: 'Объектов',
        icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M10,2V4.26L12,5.59V4H22V19H17V21H24V2H10M7.5,5L0,10V21H15V10L7.5,5M14,6V6.93L15.61,8H16V6H14M18,6V8H20V6H18M7.5,7.5L13,11V19H10V13H5V19H2V11L7.5,7.5M18,10V12H20V10H18M18,14V16H20V14H18Z"/></svg>`
      }
    ])
    
    const mapPoints = ref([
      { id: 1, country: 'Россия', left: '55%', top: '30%', projects: 120, companies: 45 },
      { id: 2, country: 'Турция', left: '52%', top: '40%', projects: 85, companies: 32 },
      { id: 3, country: 'ОАЭ', left: '60%', top: '50%', projects: 95, companies: 28 },
      { id: 4, country: 'Кипр', left: '51%', top: '45%', projects: 65, companies: 22 },
      { id: 5, country: 'Грузия', left: '56%', top: '42%', projects: 45, companies: 18 },
      { id: 6, country: 'Черногория', left: '48%', top: '43%', projects: 35, companies: 15 },
      { id: 7, country: 'Португалия', left: '30%', top: '42%', projects: 55, companies: 20 }
    ])
    
    const connectionPaths = ref([
      'M 100 100 Q 200 50 300 150',
      'M 300 200 Q 400 100 500 250',
      'M 500 150 Q 600 200 700 100',
      'M 200 300 Q 350 250 500 350'
    ])
    
    const countries = [
      'Россия', 'Турция', 'ОАЭ', 'Кипр', 'Грузия', 
      'Черногория', 'Португалия', 'Испания', 'Италия',
      'Греция', 'Болгария', 'Сербия', 'Северный Кипр',
      'Таиланд', 'Египет'
    ]
    
    const getContinentStyle = (index) => {
      const size = Math.random() * 120 + 60
      const x = Math.random() * 100
      const y = Math.random() * 100
      const duration = Math.random() * 30 + 20
      const delay = Math.random() * 5
      
      return {
        width: `${size}px`,
        height: `${size * 0.7}px`,
        left: `${x}%`,
        top: `${y}%`,
        animationDuration: `${duration}s`,
        animationDelay: `${delay}s`
      }
    }
    
    const handleScroll = () => {
      if (geographySection.value) {
        const rect = geographySection.value.getBoundingClientRect()
        const windowHeight = window.innerHeight
        
        if (rect.top < windowHeight * 0.75 && !isVisible.value) {
          isVisible.value = true
        }
      }
    }
    
    const selectCountry = (point) => {
      selectedCountry.value = selectedCountry.value === point.country ? null : point.country
      console.log('Selected country:', point.country)
    }
    
    const showCountryInfo = (point) => {
      // Можно добавить логику показа информации
    }
    
    const hideCountryInfo = () => {
      // Можно добавить логику скрытия информации
    }
    
    const showInteractiveMap = () => {
      isMapInteractive.value = !isMapInteractive.value
    }
    
    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      handleScroll()
    })
    
    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
    })
    
    return {
      geographySection,
      isVisible,
      isMapInteractive,
      selectedCountry,
      countries,
      geographyStats,
      mapPoints,
      connectionPaths,
      openModal,
      getContinentStyle,
      selectCountry,
      showCountryInfo,
      hideCountryInfo,
      showInteractiveMap
    }
  }
}
</script>

<style scoped>
.geography {
  position: relative;
  background: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
  padding: var(--spacing-2xl) 0;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  overflow: hidden;
  color: white;
}

/* Animated Background */
.geography-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.world-grid {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 25% 25%, rgba(255, 255, 255, 0.1) 2px, transparent 2px),
    radial-gradient(circle at 75% 75%, rgba(255, 255, 255, 0.1) 2px, transparent 2px);
  background-size: 60px 60px;
  animation: gridPulse 15s ease-in-out infinite;
}

@keyframes gridPulse {
  0%, 100% { opacity: 0.3; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(1.05); }
}

.floating-continents {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.continent {
  position: absolute;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 50% 30% 70% 40%;
  animation: continentFloat 25s ease-in-out infinite;
  backdrop-filter: blur(2px);
}

@keyframes continentFloat {
  0%, 100% {
    transform: translateY(0px) rotate(0deg) scale(1);
    opacity: 0.3;
  }
  33% {
    transform: translateY(-20px) rotate(5deg) scale(1.1);
    opacity: 0.5;
  }
  66% {
    transform: translateY(-40px) rotate(-3deg) scale(0.9);
    opacity: 0.4;
  }
}

.connection-lines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.connections-svg {
  width: 100%;
  height: 100%;
}

.connection-path {
  stroke-dasharray: 10, 5;
  animation: connectionFlow 8s linear infinite;
}

@keyframes connectionFlow {
  0% {
    stroke-dashoffset: 100;
    opacity: 0.3;
  }
  50% {
    opacity: 0.8;
  }
  100% {
    stroke-dashoffset: 0;
    opacity: 0.3;
  }
}

/* Main Content */
.container {
  position: relative;
  z-index: 1;
}

/* Header */
.geography-header {
  margin-bottom: var(--spacing-2xl);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.geography-header.animate {
  opacity: 1;
  transform: translateY(0);
}

.header-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-weight: var(--font-weight-medium);
  margin-bottom: var(--spacing-lg);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  font-size: 1.1rem;
}

.badge-icon {
  animation: iconSpin 12s linear infinite;
}

@keyframes iconSpin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.geography-header h2 {
  font-size: clamp(2.8rem, 6vw, 4rem);
  color: white;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.5);
}

.section-subtitle {
  font-size: 1.3rem;
  color: rgba(255, 255, 255, 0.9);
  max-width: 900px;
  margin: 0 auto;
  line-height: 1.7;
}

/* Content Layout */
.geography-content {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: var(--spacing-2xl);
  align-items: start;
  opacity: 0;
  transform: translateY(40px);
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.2s;
}

.geography-content.animate {
  opacity: 1;
  transform: translateY(0);
}

/* Text Content */
.geography-text {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border-radius: 25px;
  padding: var(--spacing-xl);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.text-content h3 {
  font-size: 2rem;
  margin-bottom: var(--spacing-md);
  color: white;
  font-weight: var(--font-weight-semibold);
}

.text-content p {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.9);
  line-height: 1.7;
  margin-bottom: var(--spacing-lg);
}

/* Geography Stats */
.geography-stats {
  display: flex;
  gap: var(--spacing-md);
  margin-bottom: var(--spacing-lg);
}

.geography-stats .stat-item {
  flex: 1;
  text-align: center;
  padding: var(--spacing-md);
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  backdrop-filter: blur(10px);
}

.geography-stats .stat-icon {
  margin-bottom: var(--spacing-sm);
  opacity: 0.8;
}

.geography-stats .stat-content {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.geography-stats .stat-number {
  font-size: 1.8rem;
  font-weight: var(--font-weight-bold);
  color: white;
}

.geography-stats .stat-label {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.8);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Action Buttons */
.action-buttons {
  display: flex;
  gap: var(--spacing-md);
  flex-wrap: wrap;
}

.btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: var(--font-weight-medium);
  transition: all 0.3s ease;
  cursor: pointer;
}

.btn-primary {
  background: linear-gradient(135deg, var(--color-primary), #ff6b6b);
  color: white;
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
}

.btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
}

/* Interactive World Map */
.interactive-world-map {
  position: relative;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 25px;
  overflow: hidden;
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.5s ease;
}

.interactive-world-map.map-active {
  background: rgba(255, 255, 255, 0.1);
  transform: scale(1.02);
}

.map-container {
  position: relative;
  overflow: hidden;
}

.map-container img {
  width: 100%;
  height: auto;
  display: block;
  opacity: 0.8;
  transition: opacity 0.3s ease;
}

.map-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    45deg,
    rgba(15, 32, 39, 0.3) 0%,
    transparent 50%,
    rgba(44, 83, 100, 0.3) 100%
  );
}

.map-points {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* Enhanced Map Points */
.enhanced-point {
  position: absolute;
  cursor: pointer;
  z-index: 2;
  opacity: 0;
  transform: scale(0.5);
  animation: pointAppear 0.8s ease-out forwards;
}

@keyframes pointAppear {
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.point-1 { top: 30%; left: 55%; }
.point-2 { top: 40%; left: 52%; }
.point-3 { top: 50%; left: 60%; }
.point-4 { top: 45%; left: 51%; }
.point-5 { top: 42%; left: 56%; }
.point-6 { top: 43%; left: 48%; }
.point-7 { top: 42%; left: 30%; }

.point-pulse {
  position: absolute;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(216, 4, 42, 0.3);
  animation: pointPulse 2s infinite;
  transform: translate(-50%, -50%);
}

@keyframes pointPulse {
  0% {
    transform: translate(-50%, -50%) scale(0.8);
    opacity: 0.8;
  }
  50% {
    transform: translate(-50%, -50%) scale(1.5);
    opacity: 0.3;
  }
  100% {
    transform: translate(-50%, -50%) scale(2);
    opacity: 0;
  }
}

.point-core {
  position: absolute;
  width: 16px;
  height: 16px;
  background: var(--color-primary);
  border: 3px solid white;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(216, 4, 42, 0.4);
}

.enhanced-point:hover .point-core {
  transform: translate(-50%, -50%) scale(1.3);
  box-shadow: 0 6px 25px rgba(216, 4, 42, 0.6);
}

.point-tooltip {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.9);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  font-size: 0.9rem;
  white-space: nowrap;
  opacity: 0;
  transition: all 0.3s ease;
  pointer-events: none;
  backdrop-filter: blur(10px);
}

.enhanced-point:hover .point-tooltip {
  opacity: 1;
  transform: translateX(-50%) translateY(-5px);
}

/* Map Legend */
.map-legend {
  padding: var(--spacing-md);
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(10px);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.map-legend h4 {
  color: white;
  margin-bottom: var(--spacing-sm);
  font-size: 1rem;
}

.legend-items {
  display: flex;
  gap: var(--spacing-md);
  flex-wrap: wrap;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.9);
}

.legend-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid white;
}

.legend-dot.active {
  background: var(--color-primary);
}

.legend-dot.potential {
  background: rgba(255, 255, 255, 0.5);
}

/* Countries Showcase */
.countries-showcase {
  margin-top: var(--spacing-lg);
  padding: var(--spacing-lg);
  background: rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  backdrop-filter: blur(10px);
}

.showcase-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-md);
}

.showcase-header h4 {
  color: white;
  font-size: 1.3rem;
  font-weight: var(--font-weight-semibold);
}

.showcase-counter {
  background: var(--color-primary);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
}

.countries-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 0.75rem;
  margin-bottom: var(--spacing-lg);
}

.country-card {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  opacity: 0;
  transform: translateY(10px);
  animation: countryCardIn 0.6s ease-out forwards;
}

@keyframes countryCardIn {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.country-card:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

.country-card.active {
  background: rgba(216, 4, 42, 0.3);
  border-color: var(--color-primary);
}

.country-flag {
  font-size: 1.2rem;
}

.country-name {
  flex: 1;
  color: white;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
}

.country-indicator {
  width: 8px;
  height: 8px;
  background: #4ade80;
  border-radius: 50%;
  animation: indicatorPulse 2s infinite;
}

@keyframes indicatorPulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.3; }
}

.showcase-stats {
  display: flex;
  gap: var(--spacing-md);
  justify-content: center;
}

.showcase-stat {
  text-align: center;
  padding: var(--spacing-sm);
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  flex: 1;
}

.showcase-stat .stat-number {
  display: block;
  font-size: 1.5rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  margin-bottom: 0.25rem;
}

.showcase-stat .stat-text {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.8);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Responsive */
@media (max-width: 1024px) {
  .geography-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-lg);
  }
  
  .geography-stats {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
  
  .action-buttons {
    justify-content: center;
  }
}

@media (max-width: 768px) {
  .geography {
    padding: var(--spacing-xl) 0;
  }
  
  .geography-text {
    order: 2;
  }
  
  .geography-visual {
    order: 1;
  }
  
  .enhanced-point .point-core {
    width: 12px;
    height: 12px;
  }
  
  .point-tooltip {
    font-size: 0.8rem;
    padding: 0.25rem 0.75rem;
    bottom: 25px;
  }
  
  .countries-grid {
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  }
  
  .showcase-stats {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
  
  .action-buttons {
    flex-direction: column;
  }
  
  .btn {
    width: 100%;
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .geography-header h2 {
    font-size: clamp(2rem, 8vw, 3rem);
  }
  
  .text-content h3 {
    font-size: 1.5rem;
  }
  
  .geography-stats {
    grid-template-columns: 1fr;
  }
}
</style>