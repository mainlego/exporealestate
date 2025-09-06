<template>
  <section class="partners section full-width" ref="sectionRef">
    <div class="partners-background">
      <div class="network-lines">
        <div class="line" v-for="n in 8" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               animationDelay: Math.random() * 3 + 's',
               animationDuration: (6 + Math.random() * 4) + 's'
             }"></div>
      </div>
      <div class="floating-logos">
        <div class="floating-logo" v-for="n in 12" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               top: Math.random() * 100 + '%',
               animationDelay: Math.random() * 8 + 's',
               animationDuration: (15 + Math.random() * 10) + 's'
             }">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
            <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
          </svg>
        </div>
      </div>
      <div class="partners-glow"></div>
    </div>

    <div class="container">
      <div class="section-header text-center" :class="{ visible: isVisible }">
        <div class="section-badge">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2"/>
            <circle cx="9" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
            <path d="M23 21v-2a4 4 0 0 0-3-3.87" stroke="currentColor" stroke-width="2"/>
            <path d="M16 3.13a4 4 0 0 1 0 7.75" stroke="currentColor" stroke-width="2"/>
          </svg>
          Надёжные партнёры
        </div>
        <h2>Мировые лидеры<br><span class="highlight">рынка недвижимости</span></h2>
        <p class="section-subtitle">Мы гордимся сотрудничеством с ведущими компаниями и брендами мира</p>
      </div>
      
      <div class="partners-showcase" :class="{ visible: isVisible }">
        <div class="showcase-stats">
          <div class="stat-item">
            <div class="stat-icon">
              <svg width="30" height="30" viewBox="0 0 24 24" fill="none">
                <path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M6 12h4m0 0h4m-4 0v4m-4-8h8" stroke="currentColor" stroke-width="2"/>
              </svg>
            </div>
            <div class="stat-content">
              <span class="stat-number">{{ animatedStats.companies }}</span>
              <span class="stat-label">Компаний-партнёров</span>
            </div>
          </div>
          <div class="stat-item">
            <div class="stat-icon">
              <svg width="30" height="30" viewBox="0 0 24 24" fill="none">
                <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M8 14s1.5 2 4 2 4-2 4-2" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                <line x1="9" y1="9" x2="9.01" y2="9" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                <line x1="15" y1="9" x2="15.01" y2="9" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
              </svg>
            </div>
            <div class="stat-content">
              <span class="stat-number">{{ animatedStats.satisfaction }}%</span>
              <span class="stat-label">Удовлетворенность</span>
            </div>
          </div>
          <div class="stat-item">
            <div class="stat-icon">
              <svg width="30" height="30" viewBox="0 0 24 24" fill="none">
                <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z" stroke="currentColor" stroke-width="2" fill="none"/>
                <circle cx="12" cy="10" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </div>
            <div class="stat-content">
              <span class="stat-number">{{ animatedStats.countries }}+</span>
              <span class="stat-label">Стран мира</span>
            </div>
          </div>
        </div>

        <div class="partners-carousel">
          <div class="carousel-container">
            <div class="carousel-background">
              <div class="carousel-pattern"></div>
            </div>
            
            <div class="partners-track" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
              <div class="partner-slide" v-for="(slide, index) in partnerSlides" :key="index">
                <div class="partners-grid">
                  <div 
                    class="partner-logo" 
                    v-for="(partner, partnerIndex) in slide" 
                    :key="partner.id"
                    :style="{ animationDelay: (partnerIndex * 0.1) + 's' }"
                    @mouseenter="onPartnerHover(partner.id)"
                    @mouseleave="onPartnerLeave()"
                  >
                    <div class="logo-wrapper">
                      <div class="logo-glow"></div>
                      <div class="logo-content">
                        <div class="logo-placeholder">
                          <svg width="40" height="40" viewBox="0 0 24 24" fill="none">
                            <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
                            <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
                          </svg>
                        </div>
                        <div class="partner-info">
                          <h4>{{ partner.name }}</h4>
                          <p>{{ partner.category }}</p>
                        </div>
                      </div>
                      <div class="logo-overlay">
                        <div class="overlay-content">
                          <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                            <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" stroke="currentColor" stroke-width="2" fill="none"/>
                            <polyline points="15,3 21,3 21,9" stroke="currentColor" stroke-width="2" fill="none"/>
                            <line x1="10" y1="14" x2="21" y2="3" stroke="currentColor" stroke-width="2"/>
                          </svg>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="carousel-controls">
              <button class="carousel-btn prev" @click="prevSlide">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                  <path d="M15 18l-6-6 6-6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </button>
              <button class="carousel-btn next" @click="nextSlide">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                  <path d="M9 18l6-6-6-6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </button>
            </div>
          </div>
          
          <div class="carousel-indicators">
            <button 
              v-for="(slide, index) in partnerSlides" 
              :key="index"
              class="indicator" 
              :class="{ active: currentSlide === index }"
              @click="goToSlide(index)"
            >
              <span class="indicator-progress" :class="{ active: currentSlide === index }"></span>
            </button>
          </div>
        </div>

        <div class="partnership-cta">
          <div class="cta-content">
            <div class="cta-icon">
              <svg width="50" height="50" viewBox="0 0 24 24" fill="none">
                <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2"/>
                <circle cx="9" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
                <line x1="19" y1="8" x2="19" y2="14" stroke="currentColor" stroke-width="2"/>
                <line x1="22" y1="11" x2="16" y2="11" stroke="currentColor" stroke-width="2"/>
              </svg>
            </div>
            <h3>Станьте нашим партнёром</h3>
            <p>Присоединяйтесь к сети ведущих компаний рынка недвижимости</p>
            <button class="partnership-btn" @click="openPartnershipModal">
              <span>Стать партнёром</span>
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <path d="M5 12h14M12 5l7 7-7 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, onMounted, onUnmounted, inject } from 'vue'

export default {
  name: 'PartnersSection',
  setup() {
    const sectionRef = ref(null)
    const isVisible = ref(false)
    const currentSlide = ref(0)
    const hoveredPartner = ref(null)
    const openModal = inject('openModal', () => {})
    let autoSlideInterval = null
    
    const animatedStats = ref({
      companies: 0,
      satisfaction: 0,
      countries: 0
    })
    
    const partners = [
      { id: 1, name: 'Sotheby’s Realty', category: 'Премиум недвижимость' },
      { id: 2, name: 'RE/MAX', category: 'Международная сеть' },
      { id: 3, name: 'Colliers International', category: 'Коммерческая недвижимость' },
      { id: 4, name: 'CBRE Group', category: 'Управление недвижимостью' },
      { id: 5, name: 'Knight Frank', category: 'Премиум консалтинг' },
      { id: 6, name: 'JLL', category: 'Инвестиционные услуги' },
      { id: 7, name: 'Cushman & Wakefield', category: 'Коммерческая недвижимость' },
      { id: 8, name: 'Savills', category: 'Международный брокеридж' },
      { id: 9, name: 'Engel & Völkers', category: 'Премиум недвижимость' },
      { id: 10, name: 'ERA Real Estate', category: 'Риэлторская сеть' },
      { id: 11, name: 'Century 21', category: 'Международная сеть' },
      { id: 12, name: 'Keller Williams', category: 'Инновативные решения' }
    ]
    
    const partnerSlides = ref([])
    for (let i = 0; i < partners.length; i += 6) {
      partnerSlides.value.push(partners.slice(i, i + 6))
    }
    
    const goToSlide = (index) => {
      currentSlide.value = index
      stopAutoSlide()
      startAutoSlide()
    }
    
    const nextSlide = () => {
      if (currentSlide.value < partnerSlides.value.length - 1) {
        currentSlide.value++
      } else {
        currentSlide.value = 0
      }
    }
    
    const prevSlide = () => {
      if (currentSlide.value > 0) {
        currentSlide.value--
      } else {
        currentSlide.value = partnerSlides.value.length - 1
      }
    }
    
    const onPartnerHover = (partnerId) => {
      hoveredPartner.value = partnerId
    }
    
    const onPartnerLeave = () => {
      hoveredPartner.value = null
    }
    
    const openPartnershipModal = () => {
      openModal()
    }
    
    const startAutoSlide = () => {
      autoSlideInterval = setInterval(nextSlide, 4000)
    }
    
    const stopAutoSlide = () => {
      if (autoSlideInterval) {
        clearInterval(autoSlideInterval)
        autoSlideInterval = null
      }
    }
    
    const animateStats = () => {
      const duration = 2000
      const targets = { companies: 150, satisfaction: 98, countries: 35 }
      
      Object.keys(targets).forEach(key => {
        const target = targets[key]
        const start = performance.now()
        
        const animate = (now) => {
          const elapsed = now - start
          const progress = Math.min(elapsed / duration, 1)
          const easeProgress = progress * (2 - progress)
          
          animatedStats.value[key] = Math.floor(target * easeProgress)
          
          if (progress < 1) {
            requestAnimationFrame(animate)
          }
        }
        
        requestAnimationFrame(animate)
      })
    }
    
    const observeSection = () => {
      const observer = new IntersectionObserver(
        ([entry]) => {
          isVisible.value = entry.isIntersecting
          if (entry.isIntersecting) {
            setTimeout(() => animateStats(), 500)
          }
        },
        { threshold: 0.1 }
      )
      
      if (sectionRef.value) {
        observer.observe(sectionRef.value)
      }
      
      return observer
    }
    
    onMounted(() => {
      const observer = observeSection()
      startAutoSlide()
      
      onUnmounted(() => {
        observer.disconnect()
        stopAutoSlide()
      })
    })
    
    return {
      sectionRef,
      isVisible,
      currentSlide,
      partnerSlides,
      animatedStats,
      hoveredPartner,
      goToSlide,
      nextSlide,
      prevSlide,
      onPartnerHover,
      onPartnerLeave,
      openPartnershipModal
    }
  }
}
</script>

<style scoped>
.partners {
  position: relative;
  background: linear-gradient(135deg, #f8fafb 0%, #e9f4f7 100%);
  padding: var(--spacing-3xl) 0;
  overflow: hidden;
}

.partners-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.network-lines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.line {
  position: absolute;
  top: -50%;
  width: 1px;
  height: 200%;
  background: linear-gradient(180deg, transparent 0%, rgba(216, 4, 42, 0.1) 20%, rgba(216, 4, 42, 0.2) 50%, rgba(216, 4, 42, 0.1) 80%, transparent 100%);
  animation: lineFlow infinite linear;
}

@keyframes lineFlow {
  0% { 
    transform: translateY(-100%) rotate(0deg);
    opacity: 0;
  }
  10% { opacity: 1; }
  90% { opacity: 1; }
  100% { 
    transform: translateY(100%) rotate(5deg);
    opacity: 0;
  }
}

.floating-logos {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.floating-logo {
  position: absolute;
  color: rgba(216, 4, 42, 0.05);
  animation: floatLogo infinite ease-in-out;
}

.floating-logo svg {
  width: 20px;
  height: 20px;
}

@keyframes floatLogo {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
    opacity: 0.3;
  }
  25% {
    transform: translateY(-30px) rotate(90deg);
    opacity: 0.1;
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
    opacity: 0.2;
  }
  75% {
    transform: translateY(-40px) rotate(270deg);
    opacity: 0.15;
  }
}

.partners-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 800px;
  height: 400px;
  background: radial-gradient(ellipse, rgba(216, 4, 42, 0.05) 0%, transparent 70%);
  transform: translate(-50%, -50%);
  animation: glowPulse 8s ease-in-out infinite;
}

@keyframes glowPulse {
  0%, 100% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 0.5;
  }
  50% {
    transform: translate(-50%, -50%) scale(1.2);
    opacity: 0.8;
  }
}

.section-header {
  margin-bottom: var(--spacing-3xl);
  transform: translateY(30px);
  opacity: 0;
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.section-header.visible {
  transform: translateY(0);
  opacity: 1;
}

.section-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(216, 4, 42, 0.1);
  border: 1px solid rgba(216, 4, 42, 0.2);
  border-radius: 50px;
  color: var(--color-primary);
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
  margin-bottom: var(--spacing-md);
  backdrop-filter: blur(10px);
}

.section-badge svg {
  width: 16px;
  height: 16px;
}

.section-header h2 {
  font-size: clamp(2.5rem, 5vw, 4rem);
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  line-height: 1.2;
}

.section-header .highlight {
  color: var(--color-primary);
  font-weight: var(--font-weight-bold);
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--color-secondary);
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.partners-showcase {
  transform: translateY(50px);
  opacity: 0;
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.2s;
}

.partners-showcase.visible {
  transform: translateY(0);
  opacity: 1;
}

.showcase-stats {
  display: flex;
  justify-content: center;
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-3xl);
  flex-wrap: wrap;
}

.stat-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem 2rem;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(216, 4, 42, 0.1);
  transition: var(--transition);
  position: relative;
  overflow: hidden;
}

.stat-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(216, 4, 42, 0.05), transparent);
  transition: left 0.6s;
}

.stat-item:hover::before {
  left: 100%;
}

.stat-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.1);
  border-color: rgba(216, 4, 42, 0.2);
}

.stat-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 15px;
  color: white;
  box-shadow: 0 10px 30px rgba(216, 4, 42, 0.3);
}

.stat-content {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-size: 2rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-text);
  line-height: 1;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--color-secondary);
  font-weight: var(--font-weight-medium);
}

.partners-carousel {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 25px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  margin-bottom: var(--spacing-3xl);
  border: 1px solid rgba(216, 4, 42, 0.08);
  position: relative;
}

.carousel-container {
  position: relative;
}

.carousel-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.03;
}

.carousel-pattern {
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 25% 25%, var(--color-primary) 0%, transparent 50%),
    radial-gradient(circle at 75% 75%, var(--color-primary) 0%, transparent 50%);
  background-size: 100px 100px;
  animation: patternMove 20s linear infinite;
}

@keyframes patternMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(-100px, -100px); }
}

.partners-track {
  display: flex;
  transition: transform 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.partner-slide {
  min-width: 100%;
  padding: var(--spacing-xl);
}

.partners-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--spacing-lg);
  align-items: center;
  justify-items: center;
}

.partner-logo {
  position: relative;
  width: 100%;
  max-width: 300px;
  cursor: pointer;
  animation: fadeInUp 0.6s ease-out forwards;
  opacity: 0;
  transform: translateY(20px);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.logo-wrapper {
  position: relative;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 20px;
  padding: 2rem;
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  border: 2px solid transparent;
  backdrop-filter: blur(20px);
  overflow: hidden;
}

.logo-wrapper:hover {
  transform: translateY(-10px) scale(1.02);
  border-color: rgba(216, 4, 42, 0.2);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.15);
}

.logo-glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(216, 4, 42, 0.1) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.4s;
}

.logo-wrapper:hover .logo-glow {
  opacity: 1;
}

.logo-content {
  position: relative;
  z-index: 2;
  text-align: center;
}

.logo-placeholder {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto var(--spacing-md);
  color: white;
  transition: var(--transition);
}

.logo-wrapper:hover .logo-placeholder {
  transform: rotate(5deg) scale(1.1);
  box-shadow: 0 15px 30px rgba(216, 4, 42, 0.3);
}

.partner-info h4 {
  font-size: 1.1rem;
  font-weight: var(--font-weight-semibold);
  color: var(--color-text);
  margin-bottom: 0.5rem;
}

.partner-info p {
  font-size: 0.9rem;
  color: var(--color-secondary);
  font-weight: var(--font-weight-medium);
}

.logo-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, var(--color-primary), #e91e63);
  border-radius: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: all 0.3s;
}

.logo-wrapper:hover .logo-overlay {
  opacity: 0.95;
}

.overlay-content {
  color: white;
  transform: scale(0.8);
  transition: transform 0.3s;
}

.logo-wrapper:hover .overlay-content {
  transform: scale(1);
}

.carousel-controls {
  position: absolute;
  top: 50%;
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0 2rem;
  pointer-events: none;
  transform: translateY(-50%);
}

.carousel-btn {
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.95);
  border: 2px solid rgba(216, 4, 42, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: var(--transition);
  pointer-events: all;
  backdrop-filter: blur(20px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.carousel-btn:hover {
  background: var(--color-primary);
  border-color: var(--color-primary);
  color: white;
  transform: scale(1.1);
  box-shadow: 0 15px 40px rgba(216, 4, 42, 0.3);
}

.carousel-indicators {
  display: flex;
  justify-content: center;
  gap: 1rem;
  padding: var(--spacing-lg) 0;
}

.indicator {
  position: relative;
  width: 40px;
  height: 4px;
  background: rgba(216, 4, 42, 0.2);
  border: none;
  border-radius: 2px;
  cursor: pointer;
  overflow: hidden;
  transition: var(--transition);
}

.indicator-progress {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  background: var(--color-primary);
  border-radius: 2px;
  width: 0;
  transition: width 0.3s;
}

.indicator-progress.active {
  width: 100%;
}

.indicator:hover {
  background: rgba(216, 4, 42, 0.3);
  transform: scale(1.1);
}

.partnership-cta {
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 25px;
  padding: var(--spacing-xl);
  text-align: center;
  position: relative;
  overflow: hidden;
}

.partnership-cta::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: conic-gradient(from 0deg at 50% 50%, rgba(255,255,255,0.1) 0deg, transparent 60deg, rgba(255,255,255,0.1) 120deg, transparent 180deg, rgba(255,255,255,0.1) 240deg, transparent 300deg, rgba(255,255,255,0.1) 360deg);
  animation: rotateConic 8s linear infinite;
}

@keyframes rotateConic {
  to { transform: rotate(360deg); }
}

.cta-content {
  position: relative;
  z-index: 2;
  max-width: 500px;
  margin: 0 auto;
}

.cta-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 80px;
  height: 80px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  color: white;
  margin-bottom: var(--spacing-md);
  backdrop-filter: blur(20px);
  border: 2px solid rgba(255, 255, 255, 0.2);
}

.cta-content h3 {
  color: white;
  font-size: 2rem;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
}

.cta-content p {
  color: rgba(255, 255, 255, 0.9);
  font-size: 1.1rem;
  margin-bottom: var(--spacing-lg);
  line-height: 1.6;
}

.partnership-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2.5rem;
  background: rgba(255, 255, 255, 0.2);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50px;
  font-weight: var(--font-weight-semibold);
  font-size: 1.1rem;
  cursor: pointer;
  transition: var(--transition);
  backdrop-filter: blur(20px);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.partnership-btn:hover {
  background: white;
  color: var(--color-primary);
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
  border-color: white;
}

@media (max-width: 1024px) {
  .partners-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-md);
  }
  
  .showcase-stats {
    gap: var(--spacing-lg);
  }
  
  .carousel-controls {
    padding: 0 1rem;
  }
}

@media (max-width: 768px) {
  .partners {
    padding: var(--spacing-xl) 0;
  }
  
  .section-header h2 {
    font-size: clamp(2rem, 6vw, 3rem);
  }
  
  .showcase-stats {
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-md);
  }
  
  .stat-item {
    padding: 1rem 1.5rem;
    width: 100%;
    max-width: 300px;
  }
  
  .partners-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-md);
  }
  
  .partner-slide {
    padding: var(--spacing-lg);
  }
  
  .carousel-controls {
    display: none;
  }
}

@media (max-width: 480px) {
  .section-badge {
    padding: 0.5rem 1rem;
    font-size: 0.8rem;
  }
  
  .stat-icon {
    width: 50px;
    height: 50px;
  }
  
  .stat-number {
    font-size: 1.5rem;
  }
  
  .partnership-cta {
    padding: var(--spacing-lg);
  }
  
  .cta-content h3 {
    font-size: 1.5rem;
  }
  
  .partnership-btn {
    padding: 0.75rem 1.5rem;
    font-size: 1rem;
  }
}
</style>