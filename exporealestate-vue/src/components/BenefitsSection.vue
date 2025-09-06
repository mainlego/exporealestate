<template>
  <section class="benefits section full-width" ref="benefitsSection">
    <!-- Animated Background -->
    <div class="benefits-background">
      <div class="bg-shapes">
        <div class="floating-shape" v-for="n in 8" :key="n" :style="getShapeStyle(n)"></div>
      </div>
      <div class="bg-grid"></div>
    </div>
    
    <div class="container">
      <div class="section-header text-center" :class="{ 'animate': isVisible }">
        <div class="header-badge">
          <span class="badge-icon">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20 6h-2.18c.11-.31.18-.65.18-1a2.996 2.996 0 0 0-5.5-1.65l-.5.67-.5-.68C10.96 2.54 10.05 2 9 2 7.34 2 6 3.34 6 5c0 .35.07.69.18 1H4c-1.11 0-1.99.89-1.99 2L2 19c0 1.11.89 2 2 2h16c1.11 0 2-.89 2-2V8c0-1.11-.89-2-2-2zM9 4c.55 0 1 .45 1 1s-.45 1-1 1-1-.45-1-1 .45-1 1-1zm6 0c.55 0 1 .45 1 1s-.45 1-1 1-1-.45-1-1 .45-1 1-1z"/>
            </svg>
          </span>
          Преимущества участия
        </div>
        <h2>Выгода от участия</h2>
        <p class="section-subtitle">
          EXPO REAL ESTATE — не просто выставка, это инвестиция в будущее вашего бизнеса.<br>
          Вас ожидает целый ряд уникальных преимуществ:
        </p>
        <div class="header-line"></div>
      </div>
      
      <div class="benefits-grid" :class="{ 'animate': isVisible }">
        <div 
          class="benefit-card interactive" 
          v-for="(benefit, index) in benefits" 
          :key="benefit.id"
          :style="{ animationDelay: `${index * 0.15}s` }"
          @mouseenter="handleCardHover"
          @mouseleave="handleCardLeave"
        >
          <div class="card-glow"></div>
          <div class="benefit-icon" :class="benefit.iconClass">
            <component :is="benefit.icon" />
            <div class="icon-pulse"></div>
          </div>
          <div class="benefit-header">
            <h3>{{ benefit.title }}</h3>
            <div class="benefit-number">{{ String(benefit.id).padStart(2, '0') }}</div>
          </div>
          <div class="benefit-content">
            <div v-for="(item, itemIndex) in benefit.items" :key="item.title" class="benefit-item" :style="{ animationDelay: `${(index * 0.15) + (itemIndex * 0.1)}s` }">
              <div class="item-header">
                <div class="item-icon" v-html="item.iconSvg"></div>
                <h4>{{ item.title }}</h4>
              </div>
              <p>{{ item.description }}</p>
              <div class="item-progress">
                <div class="progress-bar" :style="{ width: `${item.progress || 85}%` }"></div>
              </div>
            </div>
          </div>
          <div class="card-overlay">
            <div class="overlay-content">
              <h4>{{ benefit.overlayTitle }}</h4>
              <p>{{ benefit.overlayDescription }}</p>
              <button class="btn btn-sm btn-primary" @click="openModal">Узнать больше</button>
            </div>
          </div>
        </div>
      </div>
      
      <div class="enhanced-cta-section text-center" :class="{ 'animate': isVisible }">
        <div class="cta-content">
          <div class="cta-stats">
            <div class="cta-stat" v-for="stat in ctaStats" :key="stat.id">
              <div class="stat-number">{{ stat.number }}</div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
          <h2>Присоединяйтесь к EXPO REAL ESTATE и воплотите<br>
          в жизнь инвестиционные планы, открыв новые горизонты<br>
          для вашего капитала и бизнеса.</h2>
          <div class="cta-features">
            <div class="cta-feature" v-for="feature in ctaFeatures" :key="feature.id">
              <span class="feature-icon" v-html="feature.iconSvg"></span>
              <span>{{ feature.text }}</span>
            </div>
          </div>
          <div class="cta-buttons">
            <button class="btn btn-primary btn-large" @click="openModal">
              <span class="btn-text">Получить консультацию</span>
              <span class="btn-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M20.01 15.38c-1.23 0-2.42-.2-3.53-.56-.35-.12-.74-.03-1.01.24l-1.57 1.97c-2.83-1.35-5.48-3.9-6.89-6.83l1.95-1.66c.27-.28.35-.67.24-1.02-.37-1.11-.56-2.3-.56-3.53 0-.54-.45-.99-.99-.99H4.19C3.65 3 3 3.24 3 3.99 3 13.28 10.73 21 20.01 21c.71 0 .99-.63.99-1.18v-3.45c0-.54-.45-.99-.99-.99z"/>
                </svg>
              </span>
            </button>
            <button class="btn btn-secondary btn-large" @click="scrollToNext">
              <span class="btn-text">Смотреть программу</span>
              <span class="btn-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M8.59,16.58L13.17,12L8.59,7.41L10,6L16,12L10,18L8.59,16.58Z"/>
                </svg>
              </span>
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
  name: 'BenefitsSection',
  setup() {
    const openModal = inject('openModal')
    const benefitsSection = ref(null)
    const isVisible = ref(false)
    
    const benefits = ref([
      {
        id: 1,
        title: 'Персональные консультации',
        icon: 'PersonalIcon',
        iconClass: 'personal',
        overlayTitle: 'Индивидуальный подход',
        overlayDescription: 'Персональные консультации с экспертами отрасли для максимизации ваших инвестиций',
        items: [
          {
            title: 'Экспертный Совет',
            description: 'консультации экспертов для оптимизации вашей инвестиционной стратегии и налогового планирования.',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
              <circle cx="12" cy="12" r="6" stroke="currentColor" stroke-width="2" fill="none"/>
              <circle cx="12" cy="12" r="2" fill="currentColor"/>
            </svg>`,
            progress: 92
          },
          {
            title: 'Юридическая Поддержка',
            description: 'открытие представительства вашего бизнеса за рубежом с полным юридическим сопровождением',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M9 13h6c0 .55.45 1 1 1h2c.55 0 1-.45 1-1V6c0-.55-.45-1-1-1h-2c-.55 0-1 .45-1 1v1H9V6c0-.55-.45-1-1-1H6c-.55 0-1 .45-1 1v7c0 .55.45 1 1 1h2c.55 0 1-.45 1-1z"/>
              <path d="M7 17h2v2c0 .55.45 1 1 1h4c.55 0 1-.45 1-1v-2h2c.55 0 1-.45 1-1s-.45-1-1-1H7c-.55 0-1 .45-1 1s.45 1 1 1z"/>
            </svg>`,
            progress: 88
          }
        ]
      },
      {
        id: 2,
        title: 'Комплексный подход к инвестициям',
        icon: 'InvestmentIcon',
        iconClass: 'investment',
        overlayTitle: 'Стратегические инвестиции',
        overlayDescription: 'Комплексные решения для максимизации доходности ваших инвестиций',
        items: [
          {
            title: 'Стратегическое Взаимодействие',
            description: 'переговоры напрямую лидерами отрасли и опытными инвесторами, начните совместные проекты на EXPO REAL ESTATE.',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M18 12.5c0 .83-.67 1.5-1.5 1.5s-1.5-.67-1.5-1.5.67-1.5 1.5-1.5 1.5.67 1.5 1.5zM12 4.5c-4 0-8 .5-8 4s3.58 3.5 8 3.5 8 0 8-3.5-4-4-8-4z"/>
              <path d="M21.8 16.9c-1.1-.4-2.3-.9-3.6-1.4.3-.3.5-.7.5-1.2 0-.8-.7-1.5-1.5-1.5s-1.5.7-1.5 1.5c0 .5.2.9.5 1.2-1.3.5-2.5 1-3.6 1.4-.6.2-1.2.8-1.2 1.5 0 .8.7 1.5 1.5 1.5h10c.8 0 1.5-.7 1.5-1.5 0-.7-.6-1.3-1.2-1.5z"/>
            </svg>`,
            progress: 95
          },
          {
            title: 'Инвестиционный Выбор',
            description: 'полный доступ к подборке эксклюзивных, проверенных инвестиционных возможностей в премиальной недвижимости.',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M6 2l-1.5 6L12 22l7.5-14L18 2H6zm2.38 2h7.25l.9 3.62L12 13.5 7.47 7.62L7.38 4zM12 4.25L14.75 7H9.25L12 4.25z"/>
            </svg>`,
            progress: 90
          }
        ]
      },
      {
        id: 3,
        title: 'Эксклюзивные инвестиционные предложения',
        icon: 'ExclusiveIcon',
        iconClass: 'exclusive',
        overlayTitle: 'Эксклюзивные возможности',
        overlayDescription: 'Уникальные предложения, доступные только участникам выставки',
        items: [
          {
            title: 'Лучшие Условия Покупки',
            description: 'лучшие предложения и полный доступ к специальным условиям покупки, предлагаемым только на EXPO REAL ESTATE.',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
            </svg>`,
            progress: 87
          },
          {
            title: 'Партнерские Программы',
            description: 'Воспользуйтесь специальными программами от банков-партнеров, предлагающих выгодные финансовые условия и ставки',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 3L2 8v3h20V8l-10-5zM4 13v4h2v-4H4zm4 0v4h2v-4H8zm4 0v4h2v-4h-2zm4 0v4h2v-4h-2zm4 0v4h2v-4h-2zM2 18h20v2H2v-2z"/>
            </svg>`,
            progress: 93
          }
        ]
      },
      {
        id: 4,
        title: 'Эффективность и многофункциональность',
        icon: 'EfficiencyIcon',
        iconClass: 'efficiency',
        overlayTitle: 'Максимальная эффективность',
        overlayDescription: 'Оптимизация времени и ресурсов для достижения лучших результатов',
        items: [
          {
            title: 'Оперативное Заключение Сделок',
            description: 'множество инвестиционных сделок закроются непосредственно на площадке выставки, максимально реализуя время и ресурсы.',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M7 2v11h3v9l7-12h-4l3-8z"/>
            </svg>`,
            progress: 96
          },
          {
            title: 'Интеграция цифровых решений',
            description: 'практические примеры применения цифровизации в управлении недвижимостью и оптимизации процессов',
            iconSvg: `<svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20 18c1.1 0 1.99-.9 1.99-2L22 6c0-1.1-.9-2-2-2H4c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2H0v2h24v-2h-4zM4 6h16v10H4V6z"/>
            </svg>`,
            progress: 89
          }
        ]
      }
    ])
    
    const ctaStats = ref([
      { id: 1, number: '98%', label: 'довольных клиентов' },
      { id: 2, number: '24/7', label: 'поддержка' },
      { id: 3, number: '50+', label: 'экспертов' }
    ])
    
    const ctaFeatures = ref([
      { 
        id: 1, 
        iconSvg: `<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
          <circle cx="12" cy="12" r="6" stroke="currentColor" stroke-width="2" fill="none"/>
          <circle cx="12" cy="12" r="2" fill="currentColor"/>
        </svg>`, 
        text: 'Персональный подход' 
      },
      { 
        id: 2, 
        iconSvg: `<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
        </svg>`, 
        text: 'Аналитика рынка' 
      },
      { 
        id: 3, 
        iconSvg: `<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12,17A2,2 0 0,0 14,15C14,13.89 13.1,13 12,13A2,2 0 0,0 10,15A2,2 0 0,0 12,17M18,8A2,2 0 0,1 20,10V20A2,2 0 0,1 18,22H6A2,2 0 0,1 4,20V10C4,8.89 4.9,8 6,8H7V6A5,5 0 0,1 12,1A5,5 0 0,1 17,6V8H18M12,3A3,3 0 0,0 9,6V8H15V6A3,3 0 0,0 12,3Z"/>
        </svg>`, 
        text: 'Безопасность сделок' 
      },
      { 
        id: 4, 
        iconSvg: `<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <path d="M2,21L23,12L2,3V10L17,12L2,14V21Z"/>
        </svg>`, 
        text: 'Быстрый результат' 
      }
    ])
    
    const getShapeStyle = (index) => {
      const size = Math.random() * 80 + 40
      const x = Math.random() * 100
      const y = Math.random() * 100
      const duration = Math.random() * 30 + 20
      const delay = Math.random() * 10
      
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
      if (benefitsSection.value) {
        const rect = benefitsSection.value.getBoundingClientRect()
        const windowHeight = window.innerHeight
        
        if (rect.top < windowHeight * 0.8 && !isVisible.value) {
          isVisible.value = true
        }
      }
    }
    
    const handleCardHover = (event) => {
      const card = event.currentTarget
      card.style.transform = 'translateY(-10px) scale(1.02)'
    }
    
    const handleCardLeave = (event) => {
      const card = event.currentTarget
      card.style.transform = 'translateY(0) scale(1)'
    }
    
    const scrollToNext = () => {
      const nextSection = document.querySelector('.why-visit, .participants')
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
      benefitsSection,
      isVisible,
      benefits,
      ctaStats,
      ctaFeatures,
      openModal,
      getShapeStyle,
      handleCardHover,
      handleCardLeave,
      scrollToNext
    }
  },
  components: {
    PersonalIcon: {
      template: `
        <svg width="60" height="60" viewBox="0 0 60 60" fill="none">
          <circle cx="30" cy="18" r="8" stroke="currentColor" stroke-width="2"/>
          <path d="M42 52C42 45.373 36.627 40 30 40S18 45.373 18 52" stroke="currentColor" stroke-width="2"/>
          <path d="M38 28C40 26 44 28 46 32" stroke="currentColor" stroke-width="2"/>
          <path d="M22 28C20 26 16 28 14 32" stroke="currentColor" stroke-width="2"/>
        </svg>
      `
    },
    InvestmentIcon: {
      template: `
        <svg width="60" height="60" viewBox="0 0 60 60" fill="none">
          <path d="M10 45L25 30L35 40L50 25" stroke="currentColor" stroke-width="2"/>
          <path d="M42 25H50V33" stroke="currentColor" stroke-width="2"/>
          <circle cx="30" cy="30" r="25" stroke="currentColor" stroke-width="2"/>
          <path d="M20 50L25 45L30 50L35 45L40 50" stroke="currentColor" stroke-width="2"/>
        </svg>
      `
    },
    ExclusiveIcon: {
      template: `
        <svg width="60" height="60" viewBox="0 0 60 60" fill="none">
          <path d="M30 5L35 20L50 20L38.5 30L43.5 45L30 37L16.5 45L21.5 30L10 20L25 20L30 5Z" stroke="currentColor" stroke-width="2"/>
          <circle cx="30" cy="30" r="8" stroke="currentColor" stroke-width="2"/>
        </svg>
      `
    },
    EfficiencyIcon: {
      template: `
        <svg width="60" height="60" viewBox="0 0 60 60" fill="none">
          <circle cx="30" cy="30" r="25" stroke="currentColor" stroke-width="2"/>
          <path d="M30 10V30L40 40" stroke="currentColor" stroke-width="2"/>
          <path d="M15 15L20 20" stroke="currentColor" stroke-width="2"/>
          <path d="M45 15L40 20" stroke="currentColor" stroke-width="2"/>
          <path d="M45 45L40 40" stroke="currentColor" stroke-width="2"/>
        </svg>
      `
    }
  }
}
</script>

<style scoped>
.benefits {
  position: relative;
  background: linear-gradient(135deg, #f8fafc 0%, white 50%, #f1f5f9 100%);
  padding: var(--spacing-2xl) 0;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  overflow: hidden;
}

/* Animated Background */
.benefits-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.bg-shapes {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.floating-shape {
  position: absolute;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.08), rgba(216, 4, 42, 0.04));
  border-radius: 50%;
  animation: floatBenefit 25s ease-in-out infinite;
  backdrop-filter: blur(5px);
}

@keyframes floatBenefit {
  0%, 100% { transform: translateY(0px) rotate(0deg) scale(1); opacity: 0.4; }
  33% { transform: translateY(-40px) rotate(120deg) scale(1.1); opacity: 0.7; }
  66% { transform: translateY(-80px) rotate(240deg) scale(0.9); opacity: 0.5; }
}

.bg-grid {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(rgba(216, 4, 42, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(216, 4, 42, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 30s linear infinite;
}

@keyframes gridMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

/* Main Content */
.container {
  position: relative;
  z-index: 1;
}

/* Section Header */
.section-header {
  margin-bottom: var(--spacing-2xl);
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
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1), rgba(216, 4, 42, 0.05));
  color: var(--color-primary);
  padding: 1rem 2rem;
  border-radius: 50px;
  font-weight: var(--font-weight-medium);
  margin-bottom: var(--spacing-lg);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(216, 4, 42, 0.2);
  font-size: 1.1rem;
}

.badge-icon {
  font-size: 1.3rem;
  animation: badgeFloat 4s ease-in-out infinite;
}

@keyframes badgeFloat {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-5px) rotate(5deg); }
}

.section-header h2 {
  font-size: clamp(2.8rem, 6vw, 4rem);
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  background: linear-gradient(135deg, var(--color-text) 0%, var(--color-primary) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.3rem;
  color: var(--color-secondary);
  max-width: 900px;
  margin: 0 auto var(--spacing-md);
  line-height: 1.7;
  opacity: 0.95;
}

.header-line {
  width: 120px;
  height: 4px;
  background: linear-gradient(90deg, var(--color-primary), transparent);
  margin: 0 auto;
  border-radius: 2px;
  animation: headerLineExpand 1.5s ease-out 0.5s both;
}

@keyframes headerLineExpand {
  0% { width: 0; }
  100% { width: 120px; }
}

/* Benefits Grid */
.benefits-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-2xl);
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.benefits-grid.animate {
  opacity: 1;
  transform: translateY(0);
}

/* Interactive Benefit Cards */
.benefit-card {
  position: relative;
  background: rgba(255, 255, 255, 0.9);
  padding: var(--spacing-xl);
  border-radius: 25px;
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.08),
    0 10px 20px rgba(0, 0, 0, 0.04);
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  border: 2px solid rgba(216, 4, 42, 0.1);
  overflow: hidden;
  backdrop-filter: blur(20px);
  opacity: 0;
  transform: translateY(30px) scale(0.95);
  animation: benefitCardSlideIn 0.8s ease-out forwards;
}

@keyframes benefitCardSlideIn {
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.benefit-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 6px;
  background: linear-gradient(90deg, var(--color-primary), #ff6b6b, var(--color-primary));
  background-size: 200% 100%;
  animation: benefitGradientShift 4s ease-in-out infinite;
}

@keyframes benefitGradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.benefit-card:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 
    0 30px 60px rgba(0, 0, 0, 0.15),
    0 15px 30px rgba(216, 4, 42, 0.2);
  border-color: var(--color-primary);
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

.benefit-card:hover .card-glow {
  opacity: 0.3;
  animation: glowPulse 2s ease-in-out infinite;
}

@keyframes glowPulse {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.6; }
}

/* Benefit Header */
.benefit-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--spacing-md);
}

.benefit-number {
  font-size: 2.5rem;
  font-weight: var(--font-weight-bold);
  color: rgba(216, 4, 42, 0.2);
  line-height: 1;
}

/* Enhanced Icons */
.benefit-icon {
  position: relative;
  width: 90px;
  height: 90px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: var(--spacing-md);
  color: white;
  transition: all 0.4s ease;
  overflow: hidden;
}

.benefit-icon.personal { background: linear-gradient(135deg, #667eea, #764ba2); }
.benefit-icon.investment { background: linear-gradient(135deg, #f093fb, #f5576c); }
.benefit-icon.exclusive { background: linear-gradient(135deg, #4facfe, #00f2fe); }
.benefit-icon.efficiency { background: linear-gradient(135deg, #43e97b, #38f9d7); }

.benefit-card:hover .benefit-icon {
  transform: scale(1.1) rotate(10deg);
  box-shadow: 0 15px 30px rgba(216, 4, 42, 0.3);
}

.icon-pulse {
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  animation: iconPulseAnim 3s ease-in-out infinite;
}

@keyframes iconPulseAnim {
  0%, 100% { transform: scale(1); opacity: 0.3; }
  50% { transform: scale(1.2); opacity: 0; }
}

.benefit-card h3 {
  font-size: 1.6rem;
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-semibold);
  line-height: 1.3;
  flex: 1;
}

/* Enhanced Benefit Items */
.benefit-content {
  margin-bottom: var(--spacing-lg);
}

.benefit-item {
  margin-bottom: var(--spacing-lg);
  padding: var(--spacing-md);
  background: rgba(255, 255, 255, 0.5);
  border-radius: 15px;
  border-left: 4px solid var(--color-primary);
  transition: all 0.3s ease;
  opacity: 0;
  transform: translateX(-20px);
  animation: itemSlideIn 0.6s ease-out forwards;
}

@keyframes itemSlideIn {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.benefit-item:hover {
  background: rgba(255, 255, 255, 0.8);
  transform: translateX(5px);
  box-shadow: 0 5px 15px rgba(216, 4, 42, 0.1);
}

.item-header {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  margin-bottom: var(--spacing-xs);
}

.item-icon {
  font-size: 1.5rem;
  animation: itemIconBounce 3s ease-in-out infinite;
}

@keyframes itemIconBounce {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.1); }
}

.benefit-item h4 {
  font-size: 1.2rem;
  color: var(--color-text);
  font-weight: var(--font-weight-semibold);
  flex: 1;
}

.benefit-item p {
  color: var(--color-secondary);
  line-height: 1.7;
  margin-bottom: var(--spacing-sm);
  font-size: 1rem;
}

.item-progress {
  width: 100%;
  height: 4px;
  background: rgba(216, 4, 42, 0.1);
  border-radius: 2px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, var(--color-primary), #ff6b6b);
  border-radius: 2px;
  transition: width 1.5s ease-out 0.5s;
  position: relative;
}

.progress-bar::after {
  content: '';
  position: absolute;
  top: 0;
  left: -30%;
  width: 30%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.6), transparent);
  animation: progressShine 2s ease-in-out infinite;
}

@keyframes progressShine {
  0% { left: -30%; }
  100% { left: 100%; }
}

/* Card Overlay */
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
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  opacity: 0;
  transform: scale(0.9);
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  backdrop-filter: blur(20px);
}

.benefit-card:hover .card-overlay {
  opacity: 1;
  transform: scale(1);
}

.overlay-content h4 {
  font-size: 1.8rem;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-semibold);
}

.overlay-content p {
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: var(--spacing-lg);
  opacity: 0.95;
}

.btn-sm {
  padding: 0.75rem 1.5rem;
  font-size: 0.9rem;
}

/* Enhanced CTA Section */
.enhanced-cta-section {
  padding: var(--spacing-2xl) 0;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.05) 0%, rgba(255, 255, 255, 0.9) 50%, rgba(216, 4, 42, 0.03) 100%);
  border-radius: 30px;
  margin-top: var(--spacing-2xl);
  position: relative;
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.3s;
}

.enhanced-cta-section.animate {
  opacity: 1;
  transform: translateY(0);
}

.enhanced-cta-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 30% 70%, rgba(216, 4, 42, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.cta-content {
  position: relative;
  z-index: 1;
  max-width: 1200px;
  margin: 0 auto;
}

.cta-stats {
  display: flex;
  justify-content: center;
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-xl);
}

.cta-stat {
  text-align: center;
  padding: var(--spacing-md);
  background: rgba(255, 255, 255, 0.8);
  border-radius: 15px;
  backdrop-filter: blur(10px);
  min-width: 120px;
  transition: all 0.3s ease;
}

.cta-stat:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(216, 4, 42, 0.1);
}

.stat-number {
  font-size: 2rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  margin-bottom: 0.25rem;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--color-secondary);
  opacity: 0.8;
}

.enhanced-cta-section h2 {
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  margin-bottom: var(--spacing-xl);
  color: var(--color-text);
  line-height: 1.4;
  font-weight: var(--font-weight-semibold);
}

.cta-features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-md);
  margin-bottom: var(--spacing-xl);
}

.cta-feature {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  padding: var(--spacing-md);
  background: rgba(255, 255, 255, 0.6);
  border-radius: 12px;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(216, 4, 42, 0.1);
}

.cta-feature:hover {
  background: rgba(255, 255, 255, 0.9);
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(216, 4, 42, 0.1);
}

.feature-icon {
  font-size: 1.3rem;
}

.cta-buttons {
  display: flex;
  gap: var(--spacing-md);
  justify-content: center;
  flex-wrap: wrap;
}

.btn-large {
  padding: 1.5rem 3rem;
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  border-radius: 50px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.btn-large:hover {
  transform: translateY(-3px) scale(1.05);
}

.btn-large:hover .btn-icon {
  transform: translateX(5px);
}

.btn-icon {
  transition: transform 0.3s ease;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .benefits-grid {
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: var(--spacing-lg);
  }
}

@media (max-width: 768px) {
  .benefits {
    padding: var(--spacing-xl) 0;
  }
  
  .benefits-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-md);
  }
  
  .benefit-card {
    padding: var(--spacing-lg);
  }
  
  .benefit-icon {
    width: 70px;
    height: 70px;
  }
  
  .benefit-header {
    flex-direction: column;
    align-items: flex-start;
    gap: var(--spacing-xs);
  }
  
  .benefit-number {
    font-size: 1.8rem;
  }
  
  .cta-stats {
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-md);
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

@media (max-width: 480px) {
  .section-header h2 {
    font-size: clamp(2rem, 8vw, 3rem);
  }
  
  .benefit-card {
    padding: var(--spacing-md);
  }
  
  .benefit-icon {
    width: 60px;
    height: 60px;
  }
  
  .benefit-card h3 {
    font-size: 1.3rem;
  }
}
</style>