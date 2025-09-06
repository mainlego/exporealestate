<template>
  <section class="showroom section full-width" ref="sectionRef">
    <div class="showroom-background">
      <div class="luxury-patterns">
        <div class="pattern pattern-1"></div>
        <div class="pattern pattern-2"></div>
        <div class="pattern pattern-3"></div>
      </div>
      <div class="floating-buildings">
        <div class="building" v-for="n in 8" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               top: Math.random() * 100 + '%',
               animationDelay: Math.random() * 6 + 's',
               animationDuration: (20 + Math.random() * 10) + 's'
             }">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none">
            <path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z" stroke="currentColor" stroke-width="2" fill="none"/>
            <path d="M6 12h4m0 0h4m-4 0v4m-4-8h8" stroke="currentColor" stroke-width="2"/>
          </svg>
        </div>
      </div>
      <div class="premium-glow"></div>
    </div>

    <div class="container">
      <div class="showroom-content" :class="{ visible: isVisible }">
        <div class="showroom-text">
          <div class="format-intro" :class="{ visible: isVisible }">
            <div class="section-badge">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
              </svg>
              Эксклюзивный формат
            </div>
            <h2>Уникальная выставка<br><span class="highlight">Show-room</span></h2>
            <p>Позволяет экспонентам быть участниками не только в дни проведения выставки, но и арендовать экспозицию на постоянной основе.</p>
          </div>
          
          <div class="moscow-city" :class="{ visible: isVisible }">
            <div class="city-header">
              <div class="city-icon">
                <svg width="60" height="60" viewBox="0 0 24 24" fill="none">
                  <path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z" stroke="currentColor" stroke-width="2" fill="none"/>
                  <path d="M6 12h4m0 0h4m-4 0v4m-4-8h8" stroke="currentColor" stroke-width="2"/>
                  <path d="M2 22h20" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                </svg>
              </div>
              <div>
                <h3>Премиальная площадка</h3>
                <div class="city-name">Москва Сити</div>
              </div>
            </div>
            
            <div class="advantages-grid">
              <div 
                class="advantage-card" 
                v-for="(advantage, index) in advantagesGrouped" 
                :key="index"
                :class="{ visible: isVisible }"
                :style="{ animationDelay: (index * 0.1) + 's' }"
                @mouseenter="onAdvantageHover(index)"
                @mouseleave="onAdvantageLeave()"
              >
                <div class="advantage-number">{{ String(index + 1).padStart(2, '0') }}</div>
                <div class="advantage-icon">
                  <component :is="advantage.icon" />
                </div>
                <div class="advantage-content">
                  <h4>{{ advantage.title }}</h4>
                  <ul class="advantage-items">
                    <li v-for="item in advantage.items" :key="item">
                      <svg width="12" height="12" viewBox="0 0 24 24" fill="none">
                        <path d="M20 6L9 17l-5-5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                      </svg>
                      {{ item }}
                    </li>
                  </ul>
                </div>
                <div class="card-glow"></div>
              </div>
            </div>
          </div>
          
          <div class="cta-section" :class="{ visible: isVisible }">
            <div class="cta-background">
              <div class="cta-pattern"></div>
            </div>
            <div class="cta-content">
              <div class="cta-icon">
                <svg width="50" height="50" viewBox="0 0 24 24" fill="none">
                  <path d="M22 12h-4l-3 9L9 3l-3 9H2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </div>
              <h3>Станьте частью элитного проекта</h3>
              <p>Приглашаем крупнейших игроков отрасли стать частью уникального международного инвестиционного проекта.</p>
              <button class="cta-button" @click="openModal">
                <span>Стать участником</span>
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                  <path d="M5 12h14M12 5l7 7-7 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
        
        <div class="showroom-visual" :class="{ visible: isVisible }">
          <div class="visual-container">
            <div class="image-frame">
              <div class="frame-glow"></div>
              <div class="image-wrapper">
                <img src="/assets/images/unikalnyj-format-vystavki.jpg" alt="Уникальный формат выставки" />
                <div class="image-overlay">
                  <div class="overlay-content">
                    <div class="overlay-badge">
                      <svg width="30" height="30" viewBox="0 0 24 24" fill="none">
                        <path d="M12 2L15.09 8.26L22 9L17 14L18.18 21L12 17.77L5.82 21L7 14L2 9L8.91 8.26L12 2Z" 
                              fill="currentColor" stroke="currentColor" stroke-width="2"/>
                      </svg>
                      Premium локация
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="stats-cards">
              <div class="stat-card">
                <div class="stat-icon">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                    <path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z" stroke="currentColor" stroke-width="2" fill="none"/>
                    <path d="M6 12h4m0 0h4m-4 0v4m-4-8h8" stroke="currentColor" stroke-width="2"/>
                  </svg>
                </div>
                <div class="stat-text">
                  <span class="stat-number">VIP</span>
                  <span class="stat-label">Уровень</span>
                </div>
              </div>
              <div class="stat-card">
                <div class="stat-icon">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                    <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                    <path d="M16 8h-6a2 2 0 1 0 0 4h4a2 2 0 1 1 0 4H8" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                  </svg>
                </div>
                <div class="stat-text">
                  <span class="stat-number">15</span>
                  <span class="stat-label">Стран</span>
                </div>
              </div>
              <div class="stat-card">
                <div class="stat-icon">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                    <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2"/>
                    <circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
                  </svg>
                </div>
                <div class="stat-text">
                  <span class="stat-number">Premium</span>
                  <span class="stat-label">Клиенты</span>
                </div>
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

const LocationIcon = {
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z" stroke="currentColor" stroke-width="2" fill="none"/>
      <circle cx="12" cy="10" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
    </svg>
  `
}

const NetworkIcon = {
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M16 4h6m0 0v6m0-6l-7 7-4-4-6 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      <circle cx="12" cy="12" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
      <circle cx="6" cy="18" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
      <circle cx="18" cy="6" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
    </svg>
  `
}

const BrandIcon = {
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 2L15.09 8.26L22 9L17 14L18.18 21L12 17.77L5.82 21L7 14L2 9L8.91 8.26L12 2Z" 
            fill="currentColor" stroke="currentColor" stroke-width="2"/>
    </svg>
  `
}

const BusinessIcon = {
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2"/>
      <circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M16 3.13a4 4 0 0 1 0 7.75" stroke="currentColor" stroke-width="2"/>
      <path d="M8 3.13a4 4 0 0 0 0 7.75" stroke="currentColor" stroke-width="2"/>
    </svg>
  `
}

export default {
  name: 'ShowroomSection',
  components: {
    LocationIcon,
    NetworkIcon,
    BrandIcon,
    BusinessIcon
  },
  setup() {
    const openModal = inject('openModal')
    const sectionRef = ref(null)
    const isVisible = ref(false)
    const hoveredAdvantage = ref(null)
    
    const advantagesGrouped = [
      {
        title: 'Премиум локация',
        icon: 'LocationIcon',
        items: [
          'VIP уровень выставочного комплекса',
          'Самый центр бизнеса в Москве',
          'Аккумуляция крупнейшего капитала страны'
        ]
      },
      {
        title: 'Глобальная сеть',
        icon: 'NetworkIcon',
        items: [
          'Колоссальные охваты в 15+ странах мира',
          'Постоянный трафик высокопоставленных гостей',
          'Широкое освещение в СМИ'
        ]
      },
      {
        title: 'PR & Брендинг',
        icon: 'BrandIcon',
        items: [
          'Дополнительная лояльность к бренду на рынке',
          'PR и продвижение в рекламной кампании ERE',
          'Уникальный формат show room'
        ]
      },
      {
        title: 'Бизнес-возможности',
        icon: 'BusinessIcon',
        items: [
          'Возможность аренды постоянной экспозиции',
          'Продажи до, во время и после мероприятия',
          'Премиум сегмент партнеров и участников'
        ]
      }
    ]
    
    const onAdvantageHover = (index) => {
      hoveredAdvantage.value = index
    }
    
    const onAdvantageLeave = () => {
      hoveredAdvantage.value = null
    }
    
    const observeSection = () => {
      const observer = new IntersectionObserver(
        ([entry]) => {
          isVisible.value = entry.isIntersecting
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
      
      onUnmounted(() => {
        observer.disconnect()
      })
    })
    
    return {
      sectionRef,
      isVisible,
      advantagesGrouped,
      hoveredAdvantage,
      onAdvantageHover,
      onAdvantageLeave,
      openModal
    }
  }
}
</script>

<style scoped>
.showroom {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  position: relative;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #f1f5f9 100%);
  padding: var(--spacing-xl) 0;
  overflow: hidden;
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.showroom-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.luxury-patterns {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0.03;
}

.pattern {
  position: absolute;
  background: linear-gradient(45deg, var(--color-primary), transparent, var(--color-primary));
  animation: patternMove 25s linear infinite;
}

.pattern-1 {
  width: 200px;
  height: 2px;
  top: 20%;
  left: -100px;
  animation-delay: 0s;
}

.pattern-2 {
  width: 150px;
  height: 1px;
  top: 60%;
  right: -75px;
  animation-delay: 8s;
}

.pattern-3 {
  width: 100px;
  height: 1px;
  bottom: 30%;
  left: -50px;
  animation-delay: 16s;
}

@keyframes patternMove {
  0% { transform: translateX(-100px); }
  100% { transform: translateX(calc(100vw + 100px)); }
}

.floating-buildings {
  position: absolute;
  width: 100%;
  height: 100%;
}

.building {
  position: absolute;
  color: rgba(216, 4, 42, 0.1);
  animation: buildingFloat 30s infinite linear;
}

@keyframes buildingFloat {
  0% { transform: translateY(0) rotate(0deg); opacity: 0; }
  10% { opacity: 1; }
  50% { transform: translateY(-30vh) rotate(180deg); opacity: 0.5; }
  90% { opacity: 1; }
  100% { transform: translateY(-60vh) rotate(360deg); opacity: 0; }
}

.premium-glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(216, 4, 42, 0.05) 0%, rgba(255, 215, 0, 0.03) 30%, transparent 60%);
  animation: premiumGlow 20s ease-in-out infinite alternate;
}

@keyframes premiumGlow {
  0% { transform: scale(1) rotate(0deg); }
  100% { transform: scale(1.1) rotate(10deg); }
}

.container {
  position: relative;
  z-index: 2;
}

.showroom-content {
  display: grid;
  grid-template-columns: 1.3fr 1fr;
  gap: var(--spacing-xl);
  align-items: center;
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.showroom-content.visible {
  opacity: 1;
  transform: translateY(0);
}

.format-intro {
  margin-bottom: var(--spacing-lg);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.format-intro.visible {
  opacity: 1;
  transform: translateY(0);
}

.section-badge {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(216, 4, 42, 0.2);
  padding: 12px 24px;
  border-radius: 50px;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
  color: var(--color-primary);
  margin-bottom: var(--spacing-lg);
  box-shadow: 0 10px 30px rgba(216, 4, 42, 0.1);
}

.section-badge svg {
  color: var(--color-primary);
}

.format-intro h2 {
  font-size: clamp(2.5rem, 5vw, 4rem);
  color: var(--color-text);
  margin-bottom: var(--spacing-lg);
  font-weight: var(--font-weight-bold);
  line-height: 1.2;
}

.highlight {
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: var(--font-weight-bold);
}

.format-intro p {
  font-size: 1.2rem;
  color: var(--color-secondary);
  line-height: 1.7;
  max-width: 600px;
}

.moscow-city {
  margin-bottom: var(--spacing-3xl);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s;
}

.moscow-city.visible {
  opacity: 1;
  transform: translateY(0);
}

.city-header {
  display: flex;
  align-items: center;
  gap: var(--spacing-lg);
  margin-bottom: var(--spacing-2xl);
  padding: var(--spacing-lg);
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  border: 1px solid rgba(216, 4, 42, 0.1);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
}

.city-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1) 0%, rgba(255, 140, 0, 0.1) 100%);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-primary);
  box-shadow: 0 10px 25px rgba(216, 4, 42, 0.15);
  flex-shrink: 0;
  border: 2px solid rgba(216, 4, 42, 0.2);
  transition: all 0.3s ease;
}

.city-icon svg {
  filter: drop-shadow(0 2px 4px rgba(216, 4, 42, 0.3));
  transition: all 0.3s ease;
}

.moscow-city:hover .city-icon {
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  color: white;
  border-color: var(--color-primary);
  transform: scale(1.05) rotate(5deg);
}

.moscow-city:hover .city-icon svg {
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
}

.city-header h3 {
  font-size: 1.8rem;
  color: var(--color-text);
  margin-bottom: 8px;
  font-weight: var(--font-weight-semibold);
}

.city-name {
  font-size: 2.2rem;
  font-weight: var(--font-weight-bold);
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.advantages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-md);
  margin-bottom: var(--spacing-lg);
}

.advantage-card {
  position: relative;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: var(--spacing-md);
  border: 1px solid rgba(216, 4, 42, 0.1);
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.06);
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  opacity: 0;
  transform: translateY(30px);
  overflow: hidden;
}

.advantage-card.visible {
  opacity: 1;
  transform: translateY(0);
}

.advantage-card:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 0 25px 60px rgba(216, 4, 42, 0.15);
  border-color: rgba(216, 4, 42, 0.3);
}

.advantage-number {
  position: absolute;
  top: 20px;
  right: 25px;
  font-size: 3rem;
  font-weight: var(--font-weight-bold);
  color: rgba(216, 4, 42, 0.1);
  line-height: 1;
  transition: all 0.3s ease;
}

.advantage-card:hover .advantage-number {
  color: rgba(216, 4, 42, 0.2);
  transform: scale(1.1);
}

.advantage-icon {
  width: 70px;
  height: 70px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1) 0%, rgba(255, 140, 0, 0.1) 100%);
  border-radius: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-primary);
  margin-bottom: var(--spacing-lg);
  box-shadow: 0 8px 25px rgba(216, 4, 42, 0.15);
  transition: all 0.3s ease;
  border: 2px solid rgba(216, 4, 42, 0.2);
}

.advantage-icon svg {
  filter: drop-shadow(0 2px 4px rgba(216, 4, 42, 0.3));
  transition: all 0.3s ease;
}

.advantage-card:hover .advantage-icon {
  transform: rotateY(180deg) scale(1.1);
  box-shadow: 0 12px 35px rgba(216, 4, 42, 0.4);
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  color: white;
  border-color: var(--color-primary);
}

.advantage-card:hover .advantage-icon svg {
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
}

.advantage-content h4 {
  font-size: 1.4rem;
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  line-height: 1.3;
}

.advantage-items {
  list-style: none;
  padding: 0;
}

.advantage-items li {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  margin-bottom: 12px;
  font-size: 0.95rem;
  color: var(--color-secondary);
  line-height: 1.5;
  transition: all 0.3s ease;
}

.advantage-items li:hover {
  color: var(--color-text);
  transform: translateX(5px);
}

.advantage-items li svg {
  color: var(--color-primary);
  margin-top: 2px;
  flex-shrink: 0;
}

.card-glow {
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.3), rgba(255, 140, 0, 0.3));
  border-radius: 27px;
  opacity: 0;
  filter: blur(10px);
  transition: opacity 0.3s ease;
  z-index: -1;
}

.advantage-card:hover .card-glow {
  opacity: 0.4;
}

.cta-section {
  position: relative;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 30px;
  padding: var(--spacing-3xl);
  text-align: center;
  border: 1px solid rgba(216, 4, 42, 0.1);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.4s;
}

.cta-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.cta-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  opacity: 0.03;
}

.cta-pattern {
  width: 100%;
  height: 100%;
  background-image: radial-gradient(circle at 30px 30px, rgba(216, 4, 42, 0.4) 2px, transparent 2px);
  background-size: 60px 60px;
  animation: ctaPatternMove 15s linear infinite;
}

@keyframes ctaPatternMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(60px, 60px); }
}

.cta-content {
  position: relative;
  z-index: 2;
}

.cta-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  margin: 0 auto var(--spacing-lg);
  box-shadow: 0 10px 25px rgba(216, 4, 42, 0.3);
  animation: ctaIconPulse 3s ease-in-out infinite;
}

@keyframes ctaIconPulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.cta-content h3 {
  font-size: 2rem;
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
}

.cta-content p {
  font-size: 1.2rem;
  color: var(--color-secondary);
  line-height: 1.6;
  margin-bottom: var(--spacing-xl);
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.cta-button {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  color: white;
  border: none;
  padding: 18px 36px;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: var(--font-weight-semibold);
  cursor: pointer;
  box-shadow: 0 15px 40px rgba(216, 4, 42, 0.3);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  position: relative;
  overflow: hidden;
}

.cta-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s ease;
}

.cta-button:hover::before {
  left: 100%;
}

.cta-button:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 20px 50px rgba(216, 4, 42, 0.4);
}

.cta-button svg {
  transition: transform 0.3s ease;
}

.cta-button:hover svg {
  transform: translateX(3px);
}

.showroom-visual {
  position: relative;
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.16, 1, 0.3, 1) 0.3s;
}

.showroom-visual.visible {
  opacity: 1;
  transform: translateY(0);
}

.visual-container {
  position: relative;
}

.image-frame {
  position: relative;
  margin-bottom: var(--spacing-xl);
}

.frame-glow {
  position: absolute;
  top: -20px;
  left: -20px;
  right: -20px;
  bottom: -20px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.3), rgba(255, 215, 0, 0.3));
  border-radius: 40px;
  filter: blur(25px);
  opacity: 0.6;
  animation: frameGlow 4s ease-in-out infinite alternate;
}

@keyframes frameGlow {
  0% { transform: scale(1); }
  100% { transform: scale(1.02); }
}

.image-wrapper {
  position: relative;
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 0 25px 70px rgba(0, 0, 0, 0.15);
}

.image-wrapper img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.5s ease;
}

.showroom-visual:hover .image-wrapper img {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(0, 0, 0, 0.4) 0%, rgba(216, 4, 42, 0.3) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.showroom-visual:hover .image-overlay {
  opacity: 1;
}

.overlay-content {
  text-align: center;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.showroom-visual:hover .overlay-content {
  transform: translateY(0);
}

.overlay-badge {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  color: var(--color-primary);
  padding: 12px 20px;
  border-radius: 50px;
  font-weight: var(--font-weight-bold);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

.overlay-badge svg {
  color: #ffd700;
}

.stats-cards {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.stat-card {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(216, 4, 42, 0.1);
  border-radius: 20px;
  padding: 20px;
  display: flex;
  align-items: center;
  gap: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
  animation: statCardFloat 4s ease-in-out infinite alternate;
}

.stat-card:nth-child(2) {
  animation-delay: 1s;
}

.stat-card:nth-child(3) {
  animation-delay: 2s;
}

@keyframes statCardFloat {
  0% { transform: translateY(0); }
  100% { transform: translateY(-8px); }
}

.stat-card:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 15px 40px rgba(216, 4, 42, 0.15);
}

.stat-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1) 0%, rgba(255, 140, 0, 0.1) 100%);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-primary);
  box-shadow: 0 8px 20px rgba(216, 4, 42, 0.15);
  flex-shrink: 0;
  border: 2px solid rgba(216, 4, 42, 0.2);
  transition: all 0.3s ease;
}

.stat-icon svg {
  filter: drop-shadow(0 1px 2px rgba(216, 4, 42, 0.3));
  transition: all 0.3s ease;
}

.stat-card:hover .stat-icon {
  background: linear-gradient(135deg, var(--color-primary), #ff8c00);
  color: white;
  border-color: var(--color-primary);
  transform: scale(1.1);
}

.stat-card:hover .stat-icon svg {
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
}

.stat-text {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-size: 1.4rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-text);
  line-height: 1;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--color-secondary);
  margin-top: 2px;
}

@media (max-width: 1200px) {
  .showroom-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-2xl);
  }
  
  .advantages-grid {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
  
  .stats-cards {
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: var(--spacing-lg);
  }
}

@media (max-width: 768px) {
  .showroom {
    padding: var(--spacing-2xl) 0;
  }
  
  .city-header {
    flex-direction: column;
    text-align: center;
    gap: var(--spacing-md);
  }
  
  .advantages-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-lg);
  }
  
  .advantage-card {
    padding: var(--spacing-lg);
  }
  
  .cta-section {
    padding: var(--spacing-2xl);
  }
  
  .stats-cards {
    flex-direction: column;
    align-items: center;
  }
  
  .stat-card {
    width: 100%;
    max-width: 250px;
  }
}
</style>