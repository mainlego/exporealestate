<template>
  <section class="why-visit section full-width" ref="whyVisitSection">
    <!-- Animated Background -->
    <div class="visit-background">
      <div class="bg-waves">
        <div class="wave" v-for="n in 3" :key="n" :style="getWaveStyle(n)"></div>
      </div>
      <div class="floating-elements">
        <div class="element" v-for="n in 6" :key="n" :style="getElementStyle(n)"></div>
      </div>
    </div>
    
    <div class="container">
      <div class="section-header text-center" :class="{ 'animate': isVisible }">
        <div class="header-badge">
          <span class="badge-icon">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
              <path d="M9.5,3A6.5,6.5 0 0,1 16,9.5C16,11.11 15.41,12.59 14.44,13.73L14.71,14H15.5L20.5,19L19,20.5L14,15.5V14.71L13.73,14.44C12.59,15.41 11.11,16 9.5,16A6.5,6.5 0 0,1 3,9.5A6.5,6.5 0 0,1 9.5,3M9.5,5C7,5 5,7 5,9.5C5,12 7,14 9.5,14C12,14 14,12 14,9.5C14,7 12,5 9.5,5Z"/>
            </svg>
          </span>
          Причины для участия
        </div>
        <h2>Почему стоит посетить?</h2>
        <p class="section-subtitle">
          На выставке show room недвижимости ERE Вы найдете перспективные и наиболее доходные объекты для инвестиций, 
          получите консультации экспертов, индивидуальные предложения по кредитованию и бонусы от участников, 
          а также сможете заключить любую сделку за день в рамках выставки.
        </p>
        <div class="header-stats">
          <div class="stat-item" v-for="stat in headerStats" :key="stat.id">
            <span class="stat-number">{{ stat.number }}</span>
            <span class="stat-label">{{ stat.label }}</span>
          </div>
        </div>
      </div>
      
      <div class="enhanced-slider-container" :class="{ 'animate': isVisible }">
        <div class="slider-header">
          <h3>Возможности выставки</h3>
          <div class="slider-progress">
            <div class="progress-bar" :style="{ width: `${(currentSlide + 1) / slides.length * 100}%` }"></div>
          </div>
        </div>
        
        <div class="slider-wrapper">
          <div class="slides" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
            <div class="slide" v-for="(slide, index) in slides" :key="index">
              <div class="slide-grid">
                <div 
                  class="slide-item enhanced" 
                  v-for="(item, itemIndex) in slide" 
                  :key="item.id"
                  :style="{ animationDelay: `${itemIndex * 0.1}s` }"
                  @click="handleItemClick(item)"
                >
                  <div class="item-badge" v-if="item.badge">
                    <span class="badge-text">{{ item.badge }}</span>
                  </div>
                  <div class="item-image">
                    <img :src="item.image" :alt="item.title" />
                    <div class="image-overlay">
                      <div class="overlay-icon">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="white">
                          <path d="M8.59,16.58L13.17,12L8.59,7.41L10,6L16,12L10,18L8.59,16.58Z"/>
                        </svg>
                      </div>
                    </div>
                  </div>
                  <div class="item-content">
                    <div class="item-category" v-if="item.category">
                      <span class="category-icon" v-html="item.categoryIcon"></span>
                      {{ item.category }}
                    </div>
                    <h3>{{ item.title }}</h3>
                    <div class="item-features" v-if="item.features">
                      <span class="feature" v-for="feature in item.features" :key="feature">
                        {{ feature }}
                      </span>
                    </div>
                    <div class="item-footer">
                      <div class="item-price" v-if="item.price">{{ item.price }}</div>
                      <div class="item-rating" v-if="item.rating">
                        <span class="rating-stars">★★★★★</span>
                        <span class="rating-text">{{ item.rating }}</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="enhanced-slider-controls">
          <button class="slider-btn prev" @click="prevSlide" :disabled="currentSlide === 0">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M15 18L9 12L15 6"/>
            </svg>
            <span class="btn-text">Назад</span>
          </button>
          
          <div class="slider-info">
            <div class="slide-indicator">
              <span class="current-slide">{{ currentSlide + 1 }}</span>
              <span class="divider">/</span>
              <span class="total-slides">{{ slides.length }}</span>
            </div>
            <div class="slide-title">{{ slidesTitles[currentSlide] }}</div>
          </div>
          
          <button class="slider-btn next" @click="nextSlide" :disabled="currentSlide === slides.length - 1">
            <span class="btn-text">Далее</span>
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M9 18L15 12L9 6"/>
            </svg>
          </button>
        </div>
        
        <div class="slider-navigation">
          <div class="nav-dots">
            <button 
              v-for="(slide, index) in slides" 
              :key="index"
              class="nav-dot" 
              :class="{ active: currentSlide === index }"
              @click="goToSlide(index)"
            >
              <span class="dot-number">{{ index + 1 }}</span>
            </button>
          </div>
          <button class="auto-play-btn" @click="toggleAutoPlay" :class="{ active: isAutoPlay }">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" v-if="!isAutoPlay">
              <path d="M8,5.14V19.14L19,12.14L8,5.14Z"/>
            </svg>
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" v-else>
              <path d="M14,19H18V5H14M6,19H10V5H6V19Z"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'WhyVisitSection',
  setup() {
    const whyVisitSection = ref(null)
    const isVisible = ref(false)
    const currentSlide = ref(0)
    const isAutoPlay = ref(true)
    let autoSlideInterval = null
    
    const headerStats = ref([
      { id: 1, number: '8', label: 'возможностей' },
      { id: 2, number: '100%', label: 'гарантия' },
      { id: 3, number: '24/7', label: 'поддержка' }
    ])
    
    const slidesTitles = ref([
      'Консультации и финансирование',
      'Сделки и юридическое сопровождение'
    ])
    
    const slides = ref([
      [
        {
          id: 1,
          title: 'Получить консультации по налогам, инвестициям, доходам и рискам',
          price: '< 100 ₽',
          image: '/assets/images/poluchit-konsultaczii-po-nalogam-investicziyam-dohodam-i-riskam-1024x683.jpg',
          category: 'Консультации',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12,2A2,2 0 0,1 14,4C14,4.74 13.6,5.39 13,5.73V7H14A7,7 0 0,1 21,14H22A1,1 0 0,1 23,15V18A1,1 0 0,1 22,19H21V20A2,2 0 0,1 19,22H5A2,2 0 0,1 3,20V19H2A1,1 0 0,1 1,18V15A1,1 0 0,1 2,14H3A7,7 0 0,1 10,7H11V5.73C10.4,5.39 10,4.74 10,4A2,2 0 0,1 12,2Z"/></svg>`,
          features: ['Налоговое планирование', 'Анализ рисков', 'Персональный подход'],
          rating: '4.9',
          badge: 'Популярно'
        },
        {
          id: 2,
          title: 'Выбрать наиболее выгодное предложение от банка-партнера со ставкой от 3%',
          price: '< 100 ₽',
          image: '/assets/images/vybrat-naibolee-vygodnoe-predlozhenie-ot-banka-partnera-so-stavkoj-ot-3-1024x410.jpg',
          category: 'Финансирование',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12,8A4,4 0 0,1 16,12A4,4 0 0,1 12,16A4,4 0 0,1 8,12A4,4 0 0,1 12,8M12,10A2,2 0 0,0 10,12A2,2 0 0,0 12,14A2,2 0 0,0 14,12A2,2 0 0,0 12,10M10,22C9.75,22 9.54,21.82 9.5,21.58L9.13,18.93C8.5,18.68 7.96,18.34 7.44,17.94L4.95,18.95C4.73,19.03 4.46,18.95 4.34,18.73L2.34,15.27C2.21,15.05 2.27,14.78 2.46,14.63L4.57,12.97L4.5,12L4.57,11L2.46,9.37C2.27,9.22 2.21,8.95 2.34,8.73L4.34,5.27C4.46,5.05 4.73,4.96 4.95,5.05L7.44,6.05C7.96,5.66 8.5,5.32 9.13,5.07L9.5,2.42C9.54,2.18 9.75,2 10,2H14C14.25,2 14.46,2.18 14.5,2.42L14.87,5.07C15.5,5.32 16.04,5.66 16.56,6.05L19.05,5.05C19.27,4.96 19.54,5.05 19.66,5.27L21.66,8.73C21.79,8.95 21.73,9.22 21.54,9.37L19.43,11L19.5,12L19.43,13L21.54,14.63C21.73,14.78 21.79,15.05 21.66,15.27L19.66,18.73C19.54,18.95 19.27,19.04 19.05,18.95L16.56,17.95C16.04,18.34 15.5,18.68 14.87,18.93L14.5,21.58C14.46,21.82 14.25,22 14,22H10M11.25,4L10.88,6.61C9.68,6.86 8.62,7.5 7.85,8.39L5.44,7.35L4.69,8.65L6.8,10.2C6.4,11.37 6.4,12.64 6.8,13.8L4.68,15.36L5.43,16.66L7.86,15.62C8.63,16.5 9.68,17.14 10.87,17.38L11.24,20H12.76L13.13,17.39C14.32,17.14 15.37,16.5 16.14,15.62L18.57,16.66L19.32,15.36L17.2,13.81C17.6,12.64 17.6,11.37 17.2,10.2L19.31,8.65L18.56,7.35L16.15,8.39C15.38,7.5 14.32,6.86 13.12,6.62L12.75,4H11.25Z"/></svg>`,
          features: ['Низкие ставки', 'Быстрое одобрение', 'Гибкие условия'],
          rating: '4.8'
        },
        {
          id: 3,
          title: 'Получить индивидуальное предложение от ведущих банков по ипотечному кредитованию',
          price: '< 20 ₽',
          image: '/assets/images/poluchit-individualnoe-predlozhenie-ot-vedushhih-bankov-po-ipotechnomu-kreditovaniyu.jpg',
          category: 'Ипотека',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M10,20V14H14V20H19V12H22L12,3L2,12H5V20H10Z"/></svg>`,
          features: ['Индивидуальный подход', 'Лучшие банки', 'Быстрое рассмотрение'],
          rating: '4.7',
          badge: 'Выгодно'
        },
        {
          id: 4,
          title: 'Провести сразу несколько сделок по инвестициям в рамках выставки',
          image: '/assets/images/EXPO_REAL_ESTATE.png',
          category: 'Инвестиции',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M5,6H23V18H5V6M14,9A3,3 0 0,1 17,12A3,3 0 0,1 14,15A3,3 0 0,1 11,12A3,3 0 0,1 14,9M9,8A2,2 0 0,1 7,10V14A2,2 0 0,1 9,16H19A2,2 0 0,1 21,14V10A2,2 0 0,1 19,8H9Z"/></svg>`,
          features: ['Множественные сделки', 'Прямые переговоры', 'Эксклюзивные предложения'],
          rating: '4.9'
        }
      ],
      [
        {
          id: 5,
          title: 'Заказать полное юридическое сопровождение сделки',
          image: '/assets/images/EXPO_REAL_ESTATE.png',
          category: 'Юридические услуги',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12,2L13.09,8.26L22,9L14,14.74L15.64,23.5L12,21.77L8.36,23.5L10,14.74L2,9L10.91,8.26L12,2Z"/></svg>`,
          features: ['Полное сопровождение', 'Опытные юристы', 'Гарантии безопасности'],
          rating: '4.8'
        },
        {
          id: 6,
          title: 'Получить не только консультации, но и помощь в оформлении ВНЖ, золотой визы и так далее',
          price: '< 20 000 ₽',
          image: '/assets/images/EXPO_REAL_ESTATE.png',
          category: 'ВНЖ и гражданство',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M2,3H22C23.05,3 24,3.95 24,5V19C24,20.05 23.05,21 22,21H2C0.95,21 0,20.05 0,19V5C0,3.95 0.95,3 2,3M14,6V7H22V6H14M14,8V9H21.5L22,9.5V8H14M14,10V11H21V10H14M8,13.91C6,13.91 2,15 2,17V18H14V17C14,15 10,13.91 8,13.91M8,6A3,3 0 0,0 5,9A3,3 0 0,0 8,12A3,3 0 0,0 11,9A3,3 0 0,0 8,6Z"/></svg>`,
          features: ['ВНЖ оформление', 'Золотая виза', 'Экспертное сопровождение'],
          rating: '4.6',
          badge: 'Эксклюзив'
        },
        {
          id: 7,
          title: 'Изучить лучшие предложения на рынке доходной недвижимости',
          price: '< 1000 ₽',
          image: '/assets/images/luchshie-predlozheniya-na-rynke-dohodnoj-nedvizhimosti-1024x637.jpg',
          category: 'Аналитика',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M16,6L18.29,8.29L13.41,13.17L9.41,9.17L2,16.59L3.41,18L9.41,12L13.41,16L19.71,9.71L22,12V6H16Z"/></svg>`,
          features: ['Рыночная аналитика', 'Лучшие предложения', 'Доходность анализ'],
          rating: '4.7'
        },
        {
          id: 8,
          title: 'Напрямую пообщаться с застройщиками и банком',
          image: '/assets/images/napryamuyu-poobshhatsya-s-zastrojshhikami-i-bankom-1024x575.jpg',
          category: 'Нетворкинг',
          categoryIcon: `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M16,4C18.2,4 20,5.8 20,8C20,10.2 18.2,12 16,12C13.8,12 12,10.2 12,8C12,5.8 13.8,4 16,4M16,5.9A2.1,2.1 0 0,0 13.9,8A2.1,2.1 0 0,0 16,10.1A2.1,2.1 0 0,0 18.1,8A2.1,2.1 0 0,0 16,5.9M16,13C18.7,13 24,14.3 24,17V20H8V17C8,14.3 13.3,13 16,13M16,14.9C14.2,14.9 10.9,15.8 10.9,17V18.1H21.1V17C21.1,15.8 17.8,14.9 16,14.9M8,10V7H16V5H8V2H6V5H2V7H6V10H8M9,11A1,1 0 0,0 8,12A1,1 0 0,0 9,13A1,1 0 0,0 10,12A1,1 0 0,0 9,11Z"/></svg>`,
          features: ['Прямое общение', 'Застройщики', 'Банковские представители'],
          rating: '4.9'
        }
      ]
    ])
    
    const nextSlide = () => {
      if (currentSlide.value < slides.value.length - 1) {
        currentSlide.value++
      }
    }
    
    const prevSlide = () => {
      if (currentSlide.value > 0) {
        currentSlide.value--
      }
    }
    
    const goToSlide = (index) => {
      currentSlide.value = index
      if (isAutoPlay.value) {
        stopAutoSlide()
        startAutoSlide()
      }
    }
    
    const toggleAutoPlay = () => {
      isAutoPlay.value = !isAutoPlay.value
      if (isAutoPlay.value) {
        startAutoSlide()
      } else {
        stopAutoSlide()
      }
    }
    
    const handleItemClick = (item) => {
      console.log('Clicked item:', item)
      // Здесь можно добавить дополнительную логику при клике на элемент
    }
    
    const startAutoSlide = () => {
      if (!isAutoPlay.value) return
      autoSlideInterval = setInterval(() => {
        if (currentSlide.value < slides.value.length - 1) {
          nextSlide()
        } else {
          currentSlide.value = 0
        }
      }, 6000)
    }
    
    const stopAutoSlide = () => {
      if (autoSlideInterval) {
        clearInterval(autoSlideInterval)
      }
    }
    
    const getWaveStyle = (index) => {
      const delay = index * 2
      const duration = 8 + (index * 2)
      
      return {
        animationDelay: `${delay}s`,
        animationDuration: `${duration}s`
      }
    }
    
    const getElementStyle = (index) => {
      const size = Math.random() * 60 + 30
      const x = Math.random() * 100
      const y = Math.random() * 100
      const duration = Math.random() * 25 + 15
      const delay = Math.random() * 8
      
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
      if (whyVisitSection.value) {
        const rect = whyVisitSection.value.getBoundingClientRect()
        const windowHeight = window.innerHeight
        
        if (rect.top < windowHeight * 0.7 && !isVisible.value) {
          isVisible.value = true
        }
      }
    }
    
    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
      handleScroll()
      startAutoSlide()
    })
    
    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
      stopAutoSlide()
    })
    
    return {
      whyVisitSection,
      isVisible,
      currentSlide,
      isAutoPlay,
      headerStats,
      slidesTitles,
      slides,
      nextSlide,
      prevSlide,
      goToSlide,
      toggleAutoPlay,
      handleItemClick,
      getWaveStyle,
      getElementStyle
    }
  }
}
</script>

<style scoped>
.why-visit {
  position: relative;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  padding: var(--spacing-2xl) 0;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  overflow: hidden;
}

/* Animated Background */
.visit-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.bg-waves {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.wave {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.1) 0%, transparent 70%);
  border-radius: 45%;
  animation: waveFloat 12s ease-in-out infinite;
}

.wave:nth-child(1) {
  animation-delay: 0s;
}
.wave:nth-child(2) {
  animation-delay: 2s;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.08) 0%, transparent 70%);
}
.wave:nth-child(3) {
  animation-delay: 4s;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.05) 0%, transparent 70%);
}

@keyframes waveFloat {
  0%, 100% {
    transform: translate(-30%, -30%) rotate(0deg);
  }
  33% {
    transform: translate(-40%, -20%) rotate(120deg);
  }
  66% {
    transform: translate(-20%, -40%) rotate(240deg);
  }
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.element {
  position: absolute;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  animation: elementFloat 20s ease-in-out infinite;
  backdrop-filter: blur(5px);
}

@keyframes elementFloat {
  0%, 100% {
    transform: translateY(0px) rotate(0deg) scale(1);
    opacity: 0.3;
  }
  50% {
    transform: translateY(-50px) rotate(180deg) scale(1.2);
    opacity: 0.6;
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
  background: rgba(255, 255, 255, 0.2);
  color: white;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-weight: var(--font-weight-medium);
  margin-bottom: var(--spacing-lg);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  font-size: 1.1rem;
}

.badge-icon {
  animation: badgeRotate 8s linear infinite;
}

@keyframes badgeRotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
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
  color: rgba(255, 255, 255, 0.95);
  max-width: 1000px;
  margin: 0 auto var(--spacing-lg);
  line-height: 1.7;
  text-shadow: 1px 1px 4px rgba(0, 0, 0, 0.2);
}

.header-stats {
  display: flex;
  justify-content: center;
  gap: var(--spacing-lg);
  margin-top: var(--spacing-lg);
}

.stat-item {
  text-align: center;
  padding: var(--spacing-md);
  background: rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  min-width: 100px;
}

.stat-number {
  display: block;
  font-size: 1.8rem;
  font-weight: var(--font-weight-bold);
  color: white;
  margin-bottom: 0.25rem;
}

.stat-label {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.8);
}

/* Enhanced Slider Container */
.enhanced-slider-container {
  position: relative;
  max-width: 1400px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.2s;
}

.enhanced-slider-container.animate {
  opacity: 1;
  transform: translateY(0);
}

.slider-header {
  text-align: center;
  margin-bottom: var(--spacing-xl);
}

.slider-header h3 {
  font-size: 2rem;
  color: white;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-semibold);
}

.slider-progress {
  width: 200px;
  height: 4px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 2px;
  margin: 0 auto;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, white, rgba(255, 255, 255, 0.8));
  border-radius: 2px;
  transition: width 0.5s ease;
}

/* Slider Wrapper */
.slider-wrapper {
  overflow: hidden;
  border-radius: 25px;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.slides {
  display: flex;
  transition: transform 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.slide {
  min-width: 100%;
  padding: var(--spacing-xl);
}

.slide-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-lg);
}

/* Enhanced Slide Items */
.slide-item.enhanced {
  position: relative;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.15),
    0 10px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  cursor: pointer;
  opacity: 0;
  transform: translateY(30px) scale(0.95);
  animation: slideItemIn 0.8s ease-out forwards;
}

@keyframes slideItemIn {
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.slide-item.enhanced:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 
    0 30px 60px rgba(0, 0, 0, 0.2),
    0 15px 30px rgba(0, 0, 0, 0.15);
}

.item-badge {
  position: absolute;
  top: 15px;
  right: 15px;
  background: linear-gradient(135deg, var(--color-primary), #ff6b6b);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: var(--font-weight-medium);
  z-index: 2;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Enhanced Item Image */
.item-image {
  position: relative;
  height: 220px;
  overflow: hidden;
}

.item-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.slide-item.enhanced:hover .item-image img {
  transform: scale(1.1);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    transparent 0%,
    rgba(0, 0, 0, 0.3) 70%,
    rgba(0, 0, 0, 0.6) 100%
  );
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.slide-item.enhanced:hover .image-overlay {
  opacity: 1;
}

.overlay-icon {
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: scale(0.8);
  transition: all 0.3s ease;
}

.slide-item.enhanced:hover .overlay-icon {
  transform: scale(1);
}

/* Enhanced Item Content */
.item-content {
  padding: var(--spacing-lg);
}

.item-category {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: var(--color-primary);
  font-weight: var(--font-weight-medium);
  margin-bottom: var(--spacing-sm);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.category-icon {
  opacity: 0.8;
}

.item-content h3 {
  font-size: 1.2rem;
  color: var(--color-text);
  line-height: 1.4;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-semibold);
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.item-features {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: var(--spacing-md);
}

.feature {
  padding: 0.25rem 0.75rem;
  background: var(--color-background-light);
  color: var(--color-secondary);
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: var(--font-weight-medium);
}

.item-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.item-price {
  font-size: 1.4rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
}

.item-rating {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.rating-stars {
  color: #ffc107;
  font-size: 1rem;
}

.rating-text {
  font-size: 0.9rem;
  color: var(--color-secondary);
  font-weight: var(--font-weight-medium);
}

/* Enhanced Slider Controls */
.enhanced-slider-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: var(--spacing-xl);
  padding: 0 var(--spacing-md);
}

.slider-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2rem;
  background: rgba(255, 255, 255, 0.15);
  color: white;
  border-radius: 50px;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
}

.slider-btn:hover:not(:disabled) {
  background: rgba(255, 255, 255, 0.25);
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

.slider-btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.slider-info {
  text-align: center;
  color: white;
}

.slide-indicator {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 0.5rem;
}

.current-slide {
  font-size: 1.5rem;
  font-weight: var(--font-weight-bold);
}

.divider {
  font-size: 1.2rem;
  opacity: 0.7;
}

.total-slides {
  font-size: 1rem;
  opacity: 0.8;
}

.slide-title {
  font-size: 0.9rem;
  opacity: 0.9;
  font-weight: var(--font-weight-medium);
}

/* Slider Navigation */
.slider-navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: var(--spacing-lg);
}

.nav-dots {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex: 1;
}

.nav-dot {
  position: relative;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(10px);
}

.nav-dot.active {
  background: rgba(255, 255, 255, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
  transform: scale(1.2);
}

.nav-dot:hover {
  background: rgba(255, 255, 255, 0.25);
  transform: scale(1.1);
}

.dot-number {
  color: white;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
}

.auto-play-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.3);
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(10px);
}

.auto-play-btn.active {
  background: rgba(255, 255, 255, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
}

.auto-play-btn:hover {
  background: rgba(255, 255, 255, 0.25);
  transform: scale(1.1);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .slide-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--spacing-md);
  }
}

@media (max-width: 768px) {
  .why-visit {
    padding: var(--spacing-xl) 0;
  }
  
  .header-stats {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
  
  .slide-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-md);
  }
  
  .slide {
    padding: var(--spacing-md);
  }
  
  .item-image {
    height: 180px;
  }
  
  .enhanced-slider-controls {
    flex-direction: column;
    gap: var(--spacing-md);
  }
  
  .slider-btn {
    padding: 0.75rem 1.5rem;
    font-size: 0.8rem;
  }
  
  .nav-dots {
    gap: 0.5rem;
  }
  
  .nav-dot {
    width: 35px;
    height: 35px;
  }
}

@media (max-width: 480px) {
  .section-header h2 {
    font-size: clamp(2rem, 8vw, 3rem);
  }
  
  .item-content {
    padding: var(--spacing-md);
  }
  
  .item-content h3 {
    font-size: 1.1rem;
  }
  
  .btn-text {
    display: none;
  }
  
  .slider-btn {
    padding: 0.75rem;
  }
}
</style>