<template>
  <section class="stats section full-width" ref="statsSection">
    <!-- Animated Background -->
    <div class="stats-background">
      <div class="bg-pattern"></div>
      <div class="floating-shapes">
        <div class="shape" v-for="n in 12" :key="n" :style="getShapeStyle(n)"></div>
      </div>
    </div>
    
    <!-- Main Content -->
    <div class="container">
      <!-- Intro Section -->
      <div class="stats-intro text-center" :class="{ 'animate': isVisible }">
        <div class="intro-badge">
          <span class="badge-icon">🏆</span>
          Международная выставка № 1
        </div>
        <h2>EXPO REAL ESTATE — это встречи с бизнес партнёрами со всего мира, 
        реализация доходных проектов, эффективный маркетинг, выгодные инвестиции.</h2>
        <div class="intro-line"></div>
      </div>
      
      <!-- Interactive Stats Grid -->
      <div class="stats-grid" :class="{ 'animate': isVisible }">
        <div 
          class="stat-card interactive" 
          v-for="(stat, index) in stats" 
          :key="stat.id"
          :style="{ animationDelay: `${index * 0.1}s` }"
          @mouseenter="handleStatHover(stat, $event)"
          @mouseleave="handleStatLeave"
        >
          <!-- Card Header -->
          <div class="stat-header">
            <div class="stat-icon" :class="stat.className">
              <component :is="stat.icon" />
            </div>
            <div class="stat-trend">
              <span class="trend-arrow">↗</span>
              <span class="trend-text">{{ stat.trend }}</span>
            </div>
          </div>
          
          <!-- Animated Number -->
          <div class="stat-number" :class="stat.className" ref="statNumbers">
            <span class="number-display">{{ displayNumbers[index] || '0' }}</span>
            <div class="number-particles">
              <span v-for="n in 5" :key="n" class="particle"></span>
            </div>
          </div>
          
          <!-- Content -->
          <h3 class="stat-title">{{ stat.title }}</h3>
          <p class="stat-description">{{ stat.description }}</p>
          
          <!-- Progress Bar -->
          <div class="stat-progress">
            <div class="progress-bar" :style="{ width: `${stat.progress}%` }"></div>
          </div>
          
          <!-- Interactive Overlay -->
          <div class="card-overlay">
            <div class="overlay-content">
              <h4>{{ stat.detailTitle }}</h4>
              <p>{{ stat.detailDescription }}</p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Enhanced CTA Section -->
      <div class="cta-section text-center" :class="{ 'animate': isVisible }">
        <div class="cta-content">
          <h2>Станьте частью уникального мероприятия, аналогов которому в мире еще не было.</h2>
          <div class="cta-features">
            <div class="feature-item" v-for="feature in ctaFeatures" :key="feature.id">
              <span class="feature-icon">{{ feature.icon }}</span>
              <span class="feature-text">{{ feature.text }}</span>
            </div>
          </div>
          <div class="cta-buttons">
            <button class="btn btn-primary btn-large" @click="openModal">
              <span class="btn-text">Получить билет</span>
              <span class="btn-icon">🎫</span>
            </button>
            <button class="btn btn-secondary btn-large" @click="scrollToNext">
              <span class="btn-text">Узнать больше</span>
              <span class="btn-icon">→</span>
            </button>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Scroll Progress Indicator -->
    <div class="scroll-progress" :style="{ width: `${scrollProgress}%` }"></div>
  </section>
</template>

<script>
import { ref, reactive, onMounted, onUnmounted, inject } from 'vue'

export default {
  name: 'StatsSection',
  setup() {
    const openModal = inject('openModal')
    const statsSection = ref(null)
    const isVisible = ref(false)
    const scrollProgress = ref(0)
    const displayNumbers = ref([])
    
    const stats = ref([
      {
        id: 1,
        number: '15+',
        title: 'представителей стран',
        description: 'из Турции, ОАЭ, Кипра, Грузии, Черногории, Португалии и тд.',
        className: 'countries',
        icon: 'CountriesIcon',
        trend: '+12%',
        progress: 85,
        detailTitle: 'Международное участие',
        detailDescription: 'Представители из 15+ стран мира с инвестиционными проектами'
      },
      {
        id: 2,
        number: '10000+',
        title: 'объектов недвижимости',
        description: 'Виллы, квартиры, апартаменты, коттеджные поселки, таунхаусы, небоскребы, гостиничные комплексы, деловые центры, туристические объекты, коммерческая недвижимость',
        className: 'properties',
        icon: 'PropertiesIcon',
        trend: '+25%',
        progress: 92,
        detailTitle: 'Разнообразие объектов',
        detailDescription: 'От элитных вилл до коммерческих центров'
      },
      {
        id: 3,
        number: '500+',
        title: 'участников отрасли',
        description: 'Крупнейшие международные застройщики, агентства по недвижимости, частные инвесторы и крупнейшие инвестфонды, дизайнерские и архитектурные бюро',
        className: 'participants',
        icon: 'ParticipantsIcon',
        trend: '+18%',
        progress: 78,
        detailTitle: 'Профессионалы отрасли',
        detailDescription: 'Ведущие игроки рынка недвижимости'
      },
      {
        id: 4,
        number: '30000+',
        title: 'посетителей',
        description: 'Прямые покупатели, инвесторы, брокеры, высокопоставленные гости, представители среднего и крупного бизнеса',
        className: 'visitors',
        icon: 'VisitorsIcon',
        trend: '+35%',
        progress: 95,
        detailTitle: 'Широкая аудитория',
        detailDescription: 'От частных инвесторов до крупных фондов'
      },
      {
        id: 5,
        number: '5.4',
        title: 'млрд ₽ недвижимости',
        description: 'Стоимость представленных объектов недвижимости',
        className: 'value',
        icon: 'ValueIcon',
        trend: '+42%',
        progress: 88,
        detailTitle: 'Высокая стоимость',
        detailDescription: 'Премиальные объекты с высоким потенциалом'
      },
      {
        id: 6,
        number: '20+',
        title: '% средний ROI',
        description: 'любого объекта недвижимости представленного на выставке',
        className: 'roi',
        icon: 'ROIIcon',
        trend: '+8%',
        progress: 75,
        detailTitle: 'Высокая доходность',
        detailDescription: 'Проверенные инвестиционные возможности'
      }
    ])
    
    const ctaFeatures = ref([
      { id: 1, icon: '🌟', text: 'Эксклюзивный доступ' },
      { id: 2, icon: '🤝', text: 'Прямые переговоры' },
      { id: 3, icon: '💎', text: 'VIP сервис' },
      { id: 4, icon: '📊', text: 'Аналитика рынка' }
    ])
    
    const getShapeStyle = (index) => {
      const size = Math.random() * 60 + 20
      const x = Math.random() * 100
      const y = Math.random() * 100
      const duration = Math.random() * 20 + 10
      const delay = Math.random() * 5
      
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
      if (statsSection.value) {
        const rect = statsSection.value.getBoundingClientRect()
        const windowHeight = window.innerHeight
        const elementTop = rect.top
        const elementHeight = rect.height
        
        // Visibility check
        if (elementTop < windowHeight && elementTop + elementHeight > 0) {
          if (!isVisible.value) {
            isVisible.value = true
            animateNumbers()
          }
        }
        
        // Scroll progress
        const scrolled = Math.max(0, Math.min(1, (windowHeight - elementTop) / (windowHeight + elementHeight)))
        scrollProgress.value = scrolled * 100
      }
    }
    
    const animateNumbers = () => {
      stats.value.forEach((stat, index) => {
        const targetText = stat.number
        const target = parseFloat(targetText.replace(/[^\d.]/g, ''))
        
        if (target > 0) {
          let current = 0
          const increment = target / 60
          const timer = setInterval(() => {
            current += increment
            if (current >= target) {
              current = target
              clearInterval(timer)
            }
            
            // Format number based on type
            let formattedNumber
            if (stat.className === 'value') {
              formattedNumber = current.toFixed(1)
            } else if (target >= 1000) {
              formattedNumber = Math.floor(current).toLocaleString()
            } else {
              formattedNumber = Math.floor(current).toString()
            }
            
            // Add suffix from original
            if (targetText.includes('+')) formattedNumber += '+'
            if (targetText.includes('%')) formattedNumber += '%'
            
            displayNumbers.value[index] = formattedNumber
          }, 16)
        } else {
          displayNumbers.value[index] = targetText
        }
      })
    }
    
    const handleStatHover = (stat, event) => {
      const card = event.currentTarget
      card.style.transform = 'translateY(-15px) scale(1.02)'
    }
    
    const handleStatLeave = (event) => {
      const card = event.currentTarget
      card.style.transform = 'translateY(0) scale(1)'
    }
    
    const scrollToNext = () => {
      const nextSection = document.querySelector('.benefits')
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
      statsSection,
      isVisible,
      scrollProgress,
      displayNumbers,
      stats,
      ctaFeatures,
      openModal,
      getShapeStyle,
      handleStatHover,
      handleStatLeave,
      scrollToNext
    }
  },
  components: {
    CountriesIcon: {
      template: `<svg width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M20 5L23 15H33L25 21L28 31L20 25L12 31L15 21L7 15H17L20 5Z" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
      </svg>`
    },
    PropertiesIcon: {
      template: `<svg width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M5 15L20 5L35 15V35H25V25H15V35H5V15Z" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
      </svg>`
    },
    ParticipantsIcon: {
      template: `<svg width="40" height="40" viewBox="0 0 40 40" fill="none">
        <circle cx="15" cy="12" r="5" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
        <circle cx="25" cy="12" r="5" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
        <path d="M5 35C5 28 10 23 15 23C17 23 19 24 20 25C21 24 23 23 25 23C30 23 35 28 35 35" stroke="currentColor" stroke-width="2"/>
      </svg>`
    },
    VisitorsIcon: {
      template: `<svg width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M20 20C23 20 25.5 17.5 25.5 14S23 8 20 8S14.5 10.5 14.5 14S17 20 20 20Z" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
        <path d="M32 35C32 28 26.5 23 20 23S8 28 8 35" stroke="currentColor" stroke-width="2"/>
      </svg>`
    },
    ValueIcon: {
      template: `<svg width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M20 5L35 20L20 35L5 20L20 5Z" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
        <path d="M15 17L20 12L25 17M20 12V28" stroke="currentColor" stroke-width="2"/>
      </svg>`
    },
    ROIIcon: {
      template: `<svg width="40" height="40" viewBox="0 0 40 40" fill="none">
        <path d="M35 15L25 5L15 15L10 10L5 15L15 25L25 15L35 15Z" stroke="currentColor" stroke-width="2" fill="currentColor" opacity="0.2"/>
        <path d="M8 32L32 8M28 8H32V12" stroke="currentColor" stroke-width="2"/>
      </svg>`
    }
  }
}
</script>

<style scoped>
.stats {
  position: relative;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 50%, #f5f7fa 100%);
  padding: var(--spacing-2xl) 0;
  overflow: hidden;
}

/* Animated Background */
.stats-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.bg-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 25% 25%, rgba(216, 4, 42, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 75% 75%, rgba(216, 4, 42, 0.03) 0%, transparent 50%);
  animation: patternFloat 20s ease-in-out infinite;
}

@keyframes patternFloat {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(2deg); }
}

.floating-shapes {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1), rgba(216, 4, 42, 0.05));
  border-radius: 50%;
  animation: float 15s ease-in-out infinite;
  backdrop-filter: blur(10px);
}

@keyframes float {
  0%, 100% { transform: translateY(0px) scale(1) rotate(0deg); opacity: 0.3; }
  33% { transform: translateY(-30px) scale(1.1) rotate(120deg); opacity: 0.6; }
  66% { transform: translateY(-60px) scale(0.9) rotate(240deg); opacity: 0.4; }
}

/* Main Content */
.container {
  position: relative;
  z-index: 1;
}

/* Intro Section */
.stats-intro {
  margin-bottom: var(--spacing-2xl);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.stats-intro.animate {
  opacity: 1;
  transform: translateY(0);
}

.intro-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(216, 4, 42, 0.1);
  color: var(--color-primary);
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  font-weight: var(--font-weight-medium);
  margin-bottom: var(--spacing-md);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(216, 4, 42, 0.2);
  animation: badgePulse 3s ease-in-out infinite;
}

@keyframes badgePulse {
  0%, 100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(216, 4, 42, 0.4); }
  50% { transform: scale(1.02); box-shadow: 0 0 0 10px rgba(216, 4, 42, 0); }
}

.badge-icon {
  font-size: 1.2rem;
  animation: iconSpin 4s linear infinite;
}

@keyframes iconSpin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.stats-intro h2 {
  font-size: clamp(1.8rem, 4vw, 3rem);
  color: var(--color-text);
  max-width: 1200px;
  margin: 0 auto var(--spacing-md);
  line-height: 1.3;
  font-weight: var(--font-weight-semibold);
  background: linear-gradient(135deg, var(--color-text) 0%, var(--color-primary) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.intro-line {
  width: 100px;
  height: 4px;
  background: linear-gradient(90deg, var(--color-primary), transparent);
  margin: 0 auto;
  border-radius: 2px;
  animation: lineExpand 2s ease-out;
}

@keyframes lineExpand {
  0% { width: 0; }
  100% { width: 100px; }
}

/* Stats Grid */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
  gap: var(--spacing-lg);
  margin-bottom: var(--spacing-2xl);
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.stats-grid.animate {
  opacity: 1;
  transform: translateY(0);
}

/* Interactive Stat Cards */
.stat-card {
  background: rgba(255, 255, 255, 0.95);
  padding: var(--spacing-xl);
  border-radius: 25px;
  text-align: center;
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.08),
    0 10px 20px rgba(0, 0, 0, 0.04);
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  position: relative;
  overflow: hidden;
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  opacity: 0;
  transform: translateY(30px) scale(0.95);
  animation: cardSlideIn 0.8s ease-out forwards;
}

@keyframes cardSlideIn {
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.stat-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 5px;
  background: linear-gradient(90deg, var(--color-primary), #ff6b6b, var(--color-primary));
  background-size: 200% 100%;
  animation: gradientShift 3s ease-in-out infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.stat-card:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 
    0 30px 60px rgba(0, 0, 0, 0.12),
    0 15px 30px rgba(216, 4, 42, 0.1);
}

/* Card Header */
.stat-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-md);
}

.stat-icon {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1), rgba(216, 4, 42, 0.05));
  transition: all 0.3s ease;
}

.stat-icon.countries { background: linear-gradient(135deg, rgba(255, 107, 107, 0.2), rgba(78, 205, 196, 0.2)); }
.stat-icon.properties { background: linear-gradient(135deg, rgba(132, 94, 194, 0.2), rgba(179, 156, 208, 0.2)); }
.stat-icon.participants { background: linear-gradient(135deg, rgba(255, 199, 95, 0.2), rgba(255, 142, 113, 0.2)); }
.stat-icon.visitors { background: linear-gradient(135deg, rgba(102, 126, 234, 0.2), rgba(118, 75, 162, 0.2)); }
.stat-icon.value { background: linear-gradient(135deg, rgba(240, 147, 251, 0.2), rgba(245, 87, 108, 0.2)); }
.stat-icon.roi { background: linear-gradient(135deg, rgba(79, 172, 254, 0.2), rgba(0, 242, 254, 0.2)); }

.stat-card:hover .stat-icon {
  transform: scale(1.1) rotate(10deg);
  box-shadow: 0 10px 20px rgba(216, 4, 42, 0.2);
}

.stat-trend {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  color: #22c55e;
  font-weight: var(--font-weight-medium);
}

.trend-arrow {
  font-size: 1.2rem;
  animation: arrowBounce 2s ease-in-out infinite;
}

@keyframes arrowBounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-3px); }
}

.trend-text {
  font-size: 0.85rem;
  opacity: 0.8;
}

/* Animated Numbers */
.stat-number {
  font-size: clamp(3.5rem, 8vw, 5rem);
  font-weight: var(--font-weight-bold);
  margin-bottom: var(--spacing-sm);
  line-height: 1;
  position: relative;
  overflow: hidden;
}

.number-display {
  display: inline-block;
  animation: numberGlow 3s ease-in-out infinite;
}

@keyframes numberGlow {
  0%, 100% { text-shadow: 0 0 5px rgba(216, 4, 42, 0.3); }
  50% { text-shadow: 0 0 20px rgba(216, 4, 42, 0.6), 0 0 30px rgba(216, 4, 42, 0.3); }
}

.number-particles {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

.particle {
  position: absolute;
  width: 3px;
  height: 3px;
  background: var(--color-primary);
  border-radius: 50%;
  opacity: 0;
  animation: particleFloat 3s ease-in-out infinite;
}

.particle:nth-child(1) { animation-delay: 0s; }
.particle:nth-child(2) { animation-delay: 0.6s; }
.particle:nth-child(3) { animation-delay: 1.2s; }
.particle:nth-child(4) { animation-delay: 1.8s; }
.particle:nth-child(5) { animation-delay: 2.4s; }

@keyframes particleFloat {
  0%, 100% { opacity: 0; transform: translateY(0) rotate(0deg); }
  10% { opacity: 1; }
  90% { opacity: 1; }
  100% { opacity: 0; transform: translateY(-50px) rotate(360deg); }
}

.stat-number.countries { background: linear-gradient(135deg, #FF6B6B, #4ECDC4); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
.stat-number.properties { background: linear-gradient(135deg, #845EC2, #B39CD0); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
.stat-number.participants { background: linear-gradient(135deg, #FFC75F, #FF8E71); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
.stat-number.visitors { background: linear-gradient(135deg, #667eea, #764ba2); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
.stat-number.value { background: linear-gradient(135deg, #f093fb, #f5576c); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
.stat-number.roi { background: linear-gradient(135deg, #4facfe, #00f2fe); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }

/* Content */
.stat-title {
  font-size: 1.4rem;
  color: var(--color-text);
  margin-bottom: var(--spacing-sm);
  text-transform: uppercase;
  letter-spacing: 1.2px;
  font-weight: var(--font-weight-semibold);
}

.stat-description {
  color: var(--color-secondary);
  line-height: 1.7;
  font-size: 1rem;
  margin-bottom: var(--spacing-md);
  opacity: 0.9;
}

/* Progress Bar */
.stat-progress {
  width: 100%;
  height: 6px;
  background: rgba(216, 4, 42, 0.1);
  border-radius: 3px;
  overflow: hidden;
  margin-bottom: var(--spacing-md);
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, var(--color-primary), #ff6b6b);
  border-radius: 3px;
  transition: width 2s ease-out;
  position: relative;
  overflow: hidden;
}

.progress-bar::after {
  content: '';
  position: absolute;
  top: 0;
  left: -50%;
  width: 50%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.6), transparent);
  animation: progressShine 2s ease-in-out infinite;
}

@keyframes progressShine {
  0% { left: -50%; }
  100% { left: 100%; }
}

/* Interactive Overlay */
.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.95), rgba(255, 107, 107, 0.9));
  color: white;
  padding: var(--spacing-xl);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transform: scale(0.9);
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  backdrop-filter: blur(20px);
}

.stat-card:hover .card-overlay {
  opacity: 1;
  transform: scale(1);
}

.overlay-content h4 {
  font-size: 1.5rem;
  margin-bottom: var(--spacing-sm);
  font-weight: var(--font-weight-semibold);
}

.overlay-content p {
  font-size: 1.1rem;
  line-height: 1.6;
  opacity: 0.95;
}

/* Enhanced CTA Section */
.cta-section {
  padding-top: var(--spacing-2xl);
  border-top: 2px solid rgba(216, 4, 42, 0.1);
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.3s;
}

.cta-section.animate {
  opacity: 1;
  transform: translateY(0);
}

.cta-content {
  max-width: 1000px;
  margin: 0 auto;
}

.cta-section h2 {
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  margin-bottom: var(--spacing-xl);
  color: var(--color-text);
  font-weight: var(--font-weight-semibold);
  line-height: 1.3;
}

.cta-features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--spacing-md);
  margin-bottom: var(--spacing-xl);
}

.feature-item {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  padding: var(--spacing-md);
  background: rgba(255, 255, 255, 0.8);
  border-radius: 15px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(216, 4, 42, 0.1);
  transition: all 0.3s ease;
}

.feature-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
  background: rgba(255, 255, 255, 0.95);
}

.feature-icon {
  font-size: 1.5rem;
  animation: featureIconBounce 3s ease-in-out infinite;
}

@keyframes featureIconBounce {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.1); }
}

.feature-text {
  font-weight: var(--font-weight-medium);
  color: var(--color-text);
}

.cta-buttons {
  display: flex;
  gap: var(--spacing-md);
  justify-content: center;
  flex-wrap: wrap;
}

.btn-large {
  padding: 1.5rem 3.5rem;
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
  position: relative;
  overflow: hidden;
}

.btn-large:hover .btn-icon {
  transform: translateX(5px);
}

.btn-icon {
  transition: transform 0.3s ease;
}

/* Scroll Progress Indicator */
.scroll-progress {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 4px;
  background: linear-gradient(90deg, var(--color-primary), #ff6b6b);
  transition: width 0.1s ease-out;
  z-index: 10;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .stats-grid {
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: var(--spacing-md);
  }
  
  .stat-card {
    padding: var(--spacing-lg);
  }
}

@media (max-width: 768px) {
  .stats {
    padding: var(--spacing-xl) 0;
  }
  
  .stats-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-md);
  }
  
  .stat-card {
    padding: var(--spacing-lg);
  }
  
  .stat-number {
    font-size: clamp(2.5rem, 15vw, 4rem);
  }
  
  .stat-header {
    flex-direction: column;
    gap: var(--spacing-sm);
    text-align: center;
  }
  
  .cta-features {
    grid-template-columns: 1fr;
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
  }
  
  .btn-large {
    width: 100%;
    max-width: 300px;
    justify-content: center;
  }
}
</style>