<template>
  <section class="participants section full-width" ref="participantsSection">
    <!-- Animated Background -->
    <div class="participants-background">
      <div class="bg-grid-pattern"></div>
      <div class="floating-cards">
        <div class="floating-card" v-for="n in 5" :key="n" :style="getFloatingCardStyle(n)"></div>
      </div>
      <div class="bg-particles">
        <div class="particle" v-for="n in 20" :key="n" :style="getParticleStyle(n)"></div>
      </div>
    </div>
    
    <div class="container">
      <div class="section-header text-center" :class="{ 'animate': isVisible }">
        <div class="header-badge">
          <span class="badge-icon">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12,4A4,4 0 0,1 16,8A4,4 0 0,1 12,12A4,4 0 0,1 8,8A4,4 0 0,1 12,4M12,14C16.42,14 20,15.79 20,18V20H4V18C4,15.79 7.58,14 12,14Z"/>
            </svg>
          </span>
          Наши участники
        </div>
        <h2>Категории участников</h2>
        <p class="section-subtitle">
          Элитные представители индустрии недвижимости со всего мира
        </p>
        <div class="header-decoration"></div>
      </div>
      
      <div class="participants-grid" :class="{ 'animate': isVisible }">
        <div 
          class="participant-card enhanced" 
          v-for="(participant, index) in participants" 
          :key="participant.id"
          :style="{ animationDelay: `${index * 0.15}s` }"
          @mouseenter="handleCardHover"
          @mouseleave="handleCardLeave"
        >
          <div class="card-number">{{ String(participant.id).padStart(2, '0') }}</div>
          <div class="card-glow"></div>
          
          <div class="participant-image">
            <img :src="participant.image" :alt="participant.title" />
            <div class="image-overlay">
              <div class="overlay-content">
                <span class="overlay-icon" v-html="participant.icon"></span>
                <h3>{{ participant.title }}</h3>
                <p class="overlay-description">{{ participant.shortDescription }}</p>
              </div>
            </div>
            <div class="image-frame"></div>
          </div>
          
          <div class="participant-content">
            <div class="content-header">
              <h3>{{ participant.title }}</h3>
              <div class="participant-badge">{{ participant.badge }}</div>
            </div>
            <p>{{ participant.description }}</p>
            
            <div class="participant-stats">
              <div class="stat-item" v-for="stat in participant.stats" :key="stat.label">
                <span class="stat-value">{{ stat.value }}</span>
                <span class="stat-label">{{ stat.label }}</span>
              </div>
            </div>
            
            <div class="participant-features">
              <span class="feature-tag" v-for="feature in participant.features" :key="feature">
                {{ feature }}
              </span>
            </div>
            
            <button class="participant-btn" @click="handleParticipantClick(participant)">
              <span>Подробнее</span>
              <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                <path d="M8.59,16.58L13.17,12L8.59,7.41L10,6L16,12L10,18L8.59,16.58Z"/>
              </svg>
            </button>
          </div>
          
          <div class="card-hover-effect"></div>
        </div>
      </div>
      
      <!-- Interactive Stats Section -->
      <div class="participants-stats" :class="{ 'animate': isVisible }">
        <div class="stats-container">
          <div class="stat-block" v-for="stat in globalStats" :key="stat.id">
            <div class="stat-icon" v-html="stat.icon"></div>
            <div class="stat-content">
              <span class="stat-number">{{ stat.value }}</span>
              <span class="stat-text">{{ stat.label }}</span>
            </div>
          </div>
        </div>
      </div>
      
      <!-- CTA Section -->
      <div class="participants-cta" :class="{ 'animate': isVisible }">
        <h3>Станьте частью элитного сообщества</h3>
        <p>Присоединяйтесь к лидерам рынка недвижимости</p>
        <div class="cta-buttons">
          <button class="btn btn-primary" @click="openModal">
            <span>Зарегистрироваться</span>
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
              <path d="M9,5V7H15.59L4,18.59L5.41,20L17,8.41V15H19V5H9Z"/>
            </svg>
          </button>
          <button class="btn btn-secondary" @click="scrollToNext">
            <span>Узнать больше</span>
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
              <path d="M8.59,16.58L13.17,12L8.59,7.41L10,6L16,12L10,18L8.59,16.58Z"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, onMounted, onUnmounted, inject } from 'vue'

export default {
  name: 'ParticipantsSection',
  setup() {
    const openModal = inject('openModal')
    const participantsSection = ref(null)
    const isVisible = ref(false)
    const participants = ref([
      {
        id: 1,
        title: 'Высокопоставленные гости',
        description: 'крупные политические деятели, отвечающие за реализацию инициатив в области и инвестиций и недвижимости',
        shortDescription: 'Лидеры отрасли',
        image: '/assets/images/Высокопоставленные_гости.jpg',
        badge: 'VIP',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="white">
          <path d="M5,3L4,5V12L11,20L19.09,11.91C19.66,11.34 20,10.53 20,9.65L20,5L18,3H13.65C12.77,3 11.96,3.34 11.39,3.91L5,10.3V5L5,3M7,5A1,1 0 0,1 8,6A1,1 0 0,1 7,7A1,1 0 0,1 6,6A1,1 0 0,1 7,5M13.5,10.5L11,13L8.5,10.5L10,9L12,11L15,8L16.5,9.5L13.5,12.5L16.5,15.5L15,17L12,14L10,16L8.5,14.5L11,11.5Z"/>
        </svg>`,
        stats: [
          { value: '50+', label: 'человек' },
          { value: '10+', label: 'стран' }
        ],
        features: ['Политики', 'Лидеры', 'Эксклюзив']
      },
      {
        id: 2,
        title: 'Опытные инвесторы',
        description: 'знающие как важно получить одними из первых самые выгодные предложения',
        shortDescription: 'Профессионалы рынка',
        image: '/assets/images/Опытные_инвесторы.png',
        badge: 'PRO',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="white">
          <path d="M12,2A10,10 0 0,1 22,12A10,10 0 0,1 12,22A10,10 0 0,1 2,12A10,10 0 0,1 12,2M12,4A8,8 0 0,0 4,12A8,8 0 0,0 12,20A8,8 0 0,0 20,12A8,8 0 0,0 12,4M12,6L13.5,9.3L17,9.8L14.5,12.2L15.2,15.6L12,13.9L8.8,15.6L9.5,12.2L7,9.8L10.5,9.3L12,6Z"/>
        </svg>`,
        stats: [
          { value: '200+', label: 'инвесторов' },
          { value: '$10B+', label: 'капитал' }
        ],
        features: ['Опыт', 'Капитал', 'Сделки']
      },
      {
        id: 3,
        title: 'Предприниматели, бизнесмены',
        description: 'которые готовы вложить свои денежные средства в перспективные проекты для сохранения и приумножения капитала',
        shortDescription: 'Лидеры бизнеса',
        image: '/assets/images/предприниматели_бизнесмены.jpg',
        badge: 'BUSINESS',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="white">
          <path d="M12,6A3,3 0 0,0 9,9A3,3 0 0,0 12,12A3,3 0 0,0 15,9A3,3 0 0,0 12,6M6,8.17A2.5,2.5 0 0,0 3.5,10.67A2.5,2.5 0 0,0 6,13.17C6.88,13.17 7.65,12.71 8.09,12.03C7.42,11.18 7,10.15 7,9C7,8.8 7,8.6 7.04,8.4C6.72,8.25 6.37,8.17 6,8.17M18,8.17C17.63,8.17 17.28,8.25 16.96,8.4C17,8.6 17,8.8 17,9C17,10.15 16.58,11.18 15.91,12.03C16.35,12.71 17.12,13.17 18,13.17A2.5,2.5 0 0,0 20.5,10.67A2.5,2.5 0 0,0 18,8.17M12,14C10,14 6,15 6,17V19H18V17C18,15 14,14 12,14M4.67,14.97C3,15.26 1,16.04 1,17.33V19H4V17C4,16.22 4.29,15.53 4.67,14.97M19.33,14.97C19.71,15.53 20,16.22 20,17V19H23V17.33C23,16.04 21,15.26 19.33,14.97Z"/>
        </svg>`,
        stats: [
          { value: '150+', label: 'компаний' },
          { value: '25+', label: 'отраслей' }
        ],
        features: ['Бизнес', 'Инновации', 'Рост']
      },
      {
        id: 4,
        title: 'Девелоперы, застройщики',
        description: 'презентующие свои проекты на элиту мира инвестиций',
        shortDescription: 'Новые проекты',
        image: '/assets/images/Девелоперы_застройщики.jpg',
        badge: 'DEVELOPER',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="white">
          <path d="M10,2V4.26L12,5.59V4H22V19H17V21H24V2H10M7.5,5L0,10V21H15V10L7.5,5M14,6V6.93L15.61,8H16V6H14M18,6V8H20V6H18M7.5,7.5L13,11V19H10V13H5V19H2V11L7.5,7.5M18,10V12H20V10H18M18,14V16H20V14H18Z"/>
        </svg>`,
        stats: [
          { value: '100+', label: 'проектов' },
          { value: '1M+', label: 'кв.м.' }
        ],
        features: ['Проекты', 'Строительство', 'Инновации']
      }
    ])
    
    const globalStats = ref([
      {
        id: 1,
        value: '500+',
        label: 'Участников',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12,5.5A3.5,3.5 0 0,1 15.5,9A3.5,3.5 0 0,1 12,12.5A3.5,3.5 0 0,1 8.5,9A3.5,3.5 0 0,1 12,5.5M5,8C5.56,8 6.08,8.15 6.53,8.42C6.38,9.85 6.8,11.27 7.66,12.38C7.16,13.34 6.16,14 5,14A3,3 0 0,1 2,11A3,3 0 0,1 5,8M19,8A3,3 0 0,1 22,11A3,3 0 0,1 19,14C17.84,14 16.84,13.34 16.34,12.38C17.2,11.27 17.62,9.85 17.47,8.42C17.92,8.15 18.44,8 19,8M5.5,18.25C5.5,16.18 8.41,14.5 12,14.5C15.59,14.5 18.5,16.18 18.5,18.25V20H5.5V18.25M0,20V18.5C0,17.11 1.89,15.94 4.45,15.6C3.86,16.28 3.5,17.22 3.5,18.25V20H0M24,20H20.5V18.25C20.5,17.22 20.14,16.28 19.55,15.6C22.11,15.94 24,17.11 24,18.5V20Z"/>
        </svg>`
      },
      {
        id: 2,
        value: '15+',
        label: 'Стран',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12,2C6.47,2 2,6.47 2,12C2,17.53 6.47,22 12,22C17.53,22 22,17.53 22,12C22,6.47 17.53,2 12,2M14,17H12V11H10L14,7V17Z"/>
        </svg>`
      },
      {
        id: 3,
        value: '10K+',
        label: 'Объектов',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
          <path d="M8.5,9A1.5,1.5 0 0,1 10,10.5A1.5,1.5 0 0,1 8.5,12A1.5,1.5 0 0,1 7,10.5A1.5,1.5 0 0,1 8.5,9M14.5,9A1.5,1.5 0 0,1 16,10.5A1.5,1.5 0 0,1 14.5,12A1.5,1.5 0 0,1 13,10.5A1.5,1.5 0 0,1 14.5,9M3,3H21V21H3V3M5,5V8H8V5H5M10,5V8H14V5H10M16,5V8H19V5H16M5,10V14H8V10H5M10,10V14H14V10H10M16,10V14H19V10H16M5,16V19H19V16H5Z"/>
        </svg>`
      },
      {
        id: 4,
        value: '30K+',
        label: 'Посетителей',
        icon: `<svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
          <path d="M1.5,4V5.5C1.5,9.65 3.71,13.28 7,15.3V20H22V18C22,15.34 16.67,14 14,14C14,14 13.83,14 13.75,14C9,14 5,10 5,5.5V4M14,4A4,4 0 0,0 10,8A4,4 0 0,0 14,12A4,4 0 0,0 18,8A4,4 0 0,0 14,4Z"/>
        </svg>`
      }
    ])
    
    const getFloatingCardStyle = (index) => {
      const size = Math.random() * 100 + 50
      const x = Math.random() * 100
      const y = Math.random() * 100
      const duration = Math.random() * 20 + 15
      const delay = Math.random() * 5
      
      return {
        width: `${size}px`,
        height: `${size * 1.4}px`,
        left: `${x}%`,
        top: `${y}%`,
        animationDuration: `${duration}s`,
        animationDelay: `${delay}s`
      }
    }
    
    const getParticleStyle = (index) => {
      const size = Math.random() * 4 + 2
      const x = Math.random() * 100
      const y = Math.random() * 100
      const duration = Math.random() * 15 + 10
      const delay = Math.random() * 3
      
      return {
        width: `${size}px`,
        height: `${size}px`,
        left: `${x}%`,
        top: `${y}%`,
        animationDuration: `${duration}s`,
        animationDelay: `${delay}s`
      }
    }
    
    const handleScroll = () => {
      if (participantsSection.value) {
        const rect = participantsSection.value.getBoundingClientRect()
        const windowHeight = window.innerHeight
        
        if (rect.top < windowHeight * 0.75 && !isVisible.value) {
          isVisible.value = true
        }
      }
    }
    
    const handleCardHover = (event) => {
      const card = event.currentTarget
      card.style.transform = 'translateY(-15px) scale(1.02) rotateY(5deg)'
    }
    
    const handleCardLeave = (event) => {
      const card = event.currentTarget
      card.style.transform = 'translateY(0) scale(1) rotateY(0)'
    }
    
    const handleParticipantClick = (participant) => {
      console.log('Clicked participant:', participant)
      openModal()
    }
    
    const scrollToNext = () => {
      const nextSection = document.querySelector('.geography')
      if (nextSection) {
        nextSection.scrollIntoView({ behavior: 'smooth' })
      }
    }
    
    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      handleScroll()
    })
    
    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
    })
    
    return {
      participantsSection,
      isVisible,
      participants,
      globalStats,
      openModal,
      getFloatingCardStyle,
      getParticleStyle,
      handleCardHover,
      handleCardLeave,
      handleParticipantClick,
      scrollToNext
    }
  }
}
</script>

<style scoped>
.participants {
  position: relative;
  background: linear-gradient(135deg, #1e3c72 0%, #2a5298 50%, #7e8ba3 100%);
  padding: var(--spacing-2xl) 0;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  overflow: hidden;
}

/* Animated Background */
.participants-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.bg-grid-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(rgba(255, 255, 255, 0.03) 2px, transparent 2px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.03) 2px, transparent 2px);
  background-size: 40px 40px;
  animation: gridSlide 20s linear infinite;
}

@keyframes gridSlide {
  0% { transform: translate(0, 0); }
  100% { transform: translate(40px, 40px); }
}

.floating-cards {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.floating-card {
  position: absolute;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
  backdrop-filter: blur(5px);
  animation: floatCard 20s ease-in-out infinite;
}

@keyframes floatCard {
  0%, 100% {
    transform: translateY(0px) rotate(0deg) scale(1);
    opacity: 0.3;
  }
  50% {
    transform: translateY(-30px) rotate(10deg) scale(1.1);
    opacity: 0.5;
  }
}

.bg-particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.particle {
  position: absolute;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 50%;
  animation: particleFloat 15s ease-in-out infinite;
}

@keyframes particleFloat {
  0%, 100% {
    transform: translateY(0px) translateX(0px);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    transform: translateY(-100px) translateX(50px);
    opacity: 0;
  }
}

/* Main Content */
.container {
  position: relative;
  z-index: 1;
}

/* Section Header */
.section-header {
  margin-bottom: var(--spacing-2xl);
  color: white;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.section-header.animate {
  opacity: 1;
  transform: translateY(0);
}

.header-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  background: rgba(255, 255, 255, 0.15);
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
  animation: iconRotate 10s linear infinite;
}

@keyframes iconRotate {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.section-header h2 {
  font-size: clamp(2.8rem, 6vw, 4rem);
  color: white;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
}

.section-subtitle {
  font-size: 1.3rem;
  color: rgba(255, 255, 255, 0.9);
  max-width: 800px;
  margin: 0 auto var(--spacing-lg);
  line-height: 1.6;
}

.header-decoration {
  width: 150px;
  height: 4px;
  background: linear-gradient(90deg, transparent, white, transparent);
  margin: 0 auto;
  border-radius: 2px;
  animation: decorationPulse 3s ease-in-out infinite;
}

@keyframes decorationPulse {
  0%, 100% { opacity: 0.5; transform: scaleX(0.8); }
  50% { opacity: 1; transform: scaleX(1); }
}

/* Participants Grid */
.participants-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-2xl);
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.participants-grid.animate {
  opacity: 1;
  transform: translateY(0);
}

/* Enhanced Participant Card */
.participant-card.enhanced {
  position: relative;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 
    0 25px 50px rgba(0, 0, 0, 0.2),
    0 15px 30px rgba(0, 0, 0, 0.15);
  transition: all 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  cursor: pointer;
  opacity: 0;
  transform: translateY(30px) scale(0.95);
  animation: cardAppear 0.8s ease-out forwards;
  transform-style: preserve-3d;
  perspective: 1000px;
}

@keyframes cardAppear {
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.participant-card.enhanced:hover {
  transform: translateY(-15px) scale(1.02) rotateY(5deg);
  box-shadow: 
    0 35px 70px rgba(0, 0, 0, 0.25),
    0 20px 40px rgba(0, 0, 0, 0.2);
}

.card-number {
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 3rem;
  font-weight: var(--font-weight-bold);
  color: rgba(216, 4, 42, 0.1);
  z-index: 1;
}

.card-glow {
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(45deg, var(--color-primary), transparent, var(--color-primary));
  border-radius: 25px;
  opacity: 0;
  z-index: -1;
  transition: opacity 0.3s ease;
}

.participant-card.enhanced:hover .card-glow {
  opacity: 0.4;
  animation: glowRotate 3s linear infinite;
}

@keyframes glowRotate {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* Enhanced Image Section */
.participant-image {
  position: relative;
  height: 280px;
  overflow: hidden;
}

.participant-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s ease;
}

.participant-card.enhanced:hover .participant-image img {
  transform: scale(1.15);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    to bottom,
    transparent 0%,
    rgba(0, 0, 0, 0.3) 50%,
    rgba(0, 0, 0, 0.8) 100%
  );
  display: flex;
  align-items: flex-end;
  padding: var(--spacing-lg);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.participant-card.enhanced:hover .image-overlay {
  opacity: 1;
}

.overlay-content {
  width: 100%;
  transform: translateY(20px);
  transition: transform 0.4s ease;
}

.participant-card.enhanced:hover .overlay-content {
  transform: translateY(0);
}

.overlay-icon {
  display: inline-block;
  margin-bottom: var(--spacing-sm);
  animation: iconBounce 2s ease-in-out infinite;
}

@keyframes iconBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-5px); }
}

.overlay-content h3 {
  color: white;
  font-size: 1.6rem;
  font-weight: var(--font-weight-semibold);
  margin-bottom: 0.5rem;
}

.overlay-description {
  color: rgba(255, 255, 255, 0.9);
  font-size: 1rem;
}

.image-frame {
  position: absolute;
  top: 10px;
  left: 10px;
  right: 10px;
  bottom: 10px;
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 15px;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.participant-card.enhanced:hover .image-frame {
  opacity: 1;
}

/* Enhanced Content */
.participant-content {
  padding: var(--spacing-xl);
}

.content-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--spacing-md);
}

.content-header h3 {
  font-size: 1.4rem;
  color: var(--color-text);
  font-weight: var(--font-weight-semibold);
  flex: 1;
}

.participant-badge {
  background: linear-gradient(135deg, var(--color-primary), #ff6b6b);
  color: white;
  padding: 0.25rem 0.75rem;
  border-radius: 15px;
  font-size: 0.75rem;
  font-weight: var(--font-weight-medium);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.participant-content p {
  color: var(--color-secondary);
  line-height: 1.7;
  font-size: 1rem;
  margin-bottom: var(--spacing-lg);
}

/* Stats Section */
.participant-stats {
  display: flex;
  gap: var(--spacing-md);
  margin-bottom: var(--spacing-md);
}

.stat-item {
  flex: 1;
  text-align: center;
  padding: var(--spacing-sm);
  background: var(--color-background-light);
  border-radius: 12px;
}

.stat-value {
  display: block;
  font-size: 1.3rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  margin-bottom: 0.25rem;
}

.stat-label {
  font-size: 0.8rem;
  color: var(--color-secondary);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Features */
.participant-features {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: var(--spacing-lg);
}

.feature-tag {
  padding: 0.25rem 0.75rem;
  background: rgba(216, 4, 42, 0.1);
  color: var(--color-primary);
  border-radius: 15px;
  font-size: 0.85rem;
  font-weight: var(--font-weight-medium);
}

/* Button */
.participant-btn {
  width: 100%;
  padding: 1rem;
  background: linear-gradient(135deg, var(--color-primary), #ff6b6b);
  color: white;
  border: none;
  border-radius: 15px;
  font-size: 1rem;
  font-weight: var(--font-weight-medium);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.participant-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(216, 4, 42, 0.3);
}

/* Hover Effect */
.card-hover-effect {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at var(--mouse-x, 50%) var(--mouse-y, 50%), rgba(216, 4, 42, 0.1) 0%, transparent 50%);
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.participant-card.enhanced:hover .card-hover-effect {
  opacity: 1;
}

/* Global Stats */
.participants-stats {
  margin-top: var(--spacing-2xl);
  padding: var(--spacing-xl);
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border-radius: 25px;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.3s;
}

.participants-stats.animate {
  opacity: 1;
  transform: translateY(0);
}

.stats-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--spacing-lg);
}

.stat-block {
  text-align: center;
  color: white;
}

.stat-block .stat-icon {
  margin-bottom: var(--spacing-sm);
  opacity: 0.8;
}

.stat-block .stat-content {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.stat-block .stat-number {
  font-size: 2.5rem;
  font-weight: var(--font-weight-bold);
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
}

.stat-block .stat-text {
  font-size: 1rem;
  opacity: 0.9;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* CTA Section */
.participants-cta {
  text-align: center;
  margin-top: var(--spacing-2xl);
  padding: var(--spacing-2xl);
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border-radius: 25px;
  color: white;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.4s;
}

.participants-cta.animate {
  opacity: 1;
  transform: translateY(0);
}

.participants-cta h3 {
  font-size: 2.2rem;
  margin-bottom: var(--spacing-sm);
  font-weight: var(--font-weight-semibold);
}

.participants-cta p {
  font-size: 1.2rem;
  margin-bottom: var(--spacing-lg);
  opacity: 0.9;
}

.cta-buttons {
  display: flex;
  gap: var(--spacing-md);
  justify-content: center;
  flex-wrap: wrap;
}

.cta-buttons .btn {
  padding: 1rem 2.5rem;
  font-size: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  border-radius: 50px;
}

.btn-primary {
  background: linear-gradient(135deg, var(--color-primary), #ff6b6b);
  color: white;
  border: none;
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
}

.btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
}

/* Responsive */
@media (max-width: 1024px) {
  .participants-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--spacing-lg);
  }
}

@media (max-width: 768px) {
  .participants {
    padding: var(--spacing-xl) 0;
  }
  
  .participants-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-md);
  }
  
  .participant-image {
    height: 220px;
  }
  
  .participant-content {
    padding: var(--spacing-lg);
  }
  
  .stats-container {
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-md);
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
  }
  
  .cta-buttons .btn {
    width: 100%;
    max-width: 300px;
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .section-header h2 {
    font-size: clamp(2rem, 8vw, 3rem);
  }
  
  .participant-stats {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
  
  .participant-features {
    justify-content: center;
  }
}
</style>