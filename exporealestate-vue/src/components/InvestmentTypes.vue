<template>
  <section class="investment-types section full-width" ref="sectionRef">
    <div class="investment-background">
      <div class="animated-shapes">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
        <div class="shape shape-4"></div>
      </div>
      <div class="floating-coins">
        <div class="coin" v-for="n in 15" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               top: Math.random() * 100 + '%',
               animationDelay: Math.random() * 8 + 's',
               animationDuration: (12 + Math.random() * 8) + 's'
             }">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
            <path d="M16 8h-6a2 2 0 1 0 0 4h4a2 2 0 1 1 0 4H8" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
            <path d="M12 6v2M12 16v2" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="section-header text-center" :class="{ visible: isVisible }">
        <div class="section-badge">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
            <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
          </svg>
          Инвестиционные возможности
        </div>
        <h2>Виды инвестирования<br><span class="highlight">в недвижимость</span></h2>
        <p class="section-subtitle">Откройте для себя разнообразные способы вложения средств в недвижимость с максимальной прибылью</p>
      </div>
      
      <div class="investment-content" :class="{ visible: isVisible }">
        <div class="investment-text">
          <div class="types-list">
            <div 
              class="type-item" 
              v-for="(type, index) in investmentTypes" 
              :key="type.id"
              :class="{ visible: isVisible }"
              :style="{ animationDelay: (index * 0.15) + 's' }"
              @mouseenter="onTypeHover(index)"
              @mouseleave="onTypeLeave()"
            >
              <div class="type-number">{{ String(type.id).padStart(2, '0') }}</div>
              <div class="type-icon">
                <div class="icon-wrapper">
                  <component :is="type.icon" />
                </div>
                <div class="icon-glow"></div>
              </div>
              <div class="type-content">
                <h3>{{ type.title }}</h3>
                <p v-if="type.description">{{ type.description }}</p>
                <div class="type-features" v-if="type.features">
                  <div v-for="feature in type.features" :key="feature" class="feature">
                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none">
                      <path d="M20 6L9 17l-5-5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                    {{ feature }}
                  </div>
                </div>
                <div class="type-progress" v-if="type.profitability">
                  <div class="progress-label">
                    <span>Доходность</span>
                    <span class="progress-value">{{ type.profitability }}</span>
                  </div>
                  <div class="progress-bar">
                    <div class="progress-fill" :style="{ width: type.progressWidth + '%' }"></div>
                  </div>
                </div>
              </div>
              <div class="type-overlay"></div>
            </div>
          </div>
        </div>
        
        <div class="investment-visual" :class="{ visible: isVisible }">
          <div class="visual-container">
            <div class="image-glow"></div>
            <div class="image-wrapper">
              <img src="/assets/images/Виды_инвестирования_в_недвижимость.jpeg" alt="Виды инвестирования" />
              <div class="image-overlay">
                <div class="overlay-content">
                  <div class="overlay-icon">
                    <svg width="60" height="60" viewBox="0 0 24 24" fill="none">
                      <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
                      <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
                    </svg>
                  </div>
                  <h3>Выберите свой способ</h3>
                  <p>Инвестируйте с умом</p>
                </div>
              </div>
            </div>
            <div class="floating-stats">
              <div class="stat-card">
                <div class="stat-icon">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M16 8h-6a2 2 0 1 0 0 4h4a2 2 0 1 1 0 4H8" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                    <path d="M12 6v2M12 16v2" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                  </svg>
                </div>
                <div class="stat-text">
                  <span class="stat-number">4%+</span>
                  <span class="stat-label">Доходность</span>
                </div>
              </div>
              <div class="stat-card">
                <div class="stat-icon">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <polyline points="23,6 13.5,15.5 8.5,10.5 1,18" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <polyline points="17,6 23,6 23,12" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </div>
                <div class="stat-text">
                  <span class="stat-number">5</span>
                  <span class="stat-label">Способов</span>
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
import { ref, onMounted, onUnmounted } from 'vue'

const CreditIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect x="2" y="4" width="20" height="16" rx="2" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M2 10h20" stroke="currentColor" stroke-width="2"/>
      <path d="M6 14h4" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
      <circle cx="16" cy="16" r="2" fill="currentColor"/>
    </svg>
  `
}

const HomeIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
    </svg>
  `
}

const BuildingIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M6 12h4m0 0h4m-4 0v4m-4-8h8" stroke="currentColor" stroke-width="2"/>
    </svg>
  `
}

const ConstructionIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z" stroke="currentColor" stroke-width="2" fill="none"/>
    </svg>
  `
}

const AuctionIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M9.5 2L8 6L12 8L16 6L14.5 2" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M12 8V22M8 18h8" stroke="currentColor" stroke-width="2"/>
      <circle cx="12" cy="18" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
    </svg>
  `
}

export default {
  name: 'InvestmentTypes',
  components: {
    CreditIcon,
    HomeIcon,
    BuildingIcon,
    ConstructionIcon,
    AuctionIcon
  },
  setup() {
    const sectionRef = ref(null)
    const isVisible = ref(false)
    const hoveredType = ref(null)
    
    const investmentTypes = [
      {
        id: 1,
        title: 'Инвестирование путем ипотечного кредитования',
        description: 'Без собственных вложений с доходностью от 4% в первый же месяц',
        icon: 'CreditIcon',
        features: ['Без первоначального взноса', 'Быстрая окупаемость', 'Минимальные риски'],
        profitability: '4%+',
        progressWidth: 75
      },
      {
        id: 2,
        title: 'Покупка жилой недвижимости для аренды',
        description: 'Стабильный пассивный доход от сдачи в аренду',
        icon: 'HomeIcon',
        features: ['Стабильный доход', 'Рост стоимости', 'Налоговые льготы'],
        profitability: '6-8%',
        progressWidth: 65
      },
      {
        id: 3,
        title: 'Коммерческая недвижимость',
        description: 'Высокая доходность от офисов, магазинов и складов',
        icon: 'BuildingIcon',
        features: ['Высокая доходность', 'Долгосрочные договоры', 'Профессиональные арендаторы'],
        profitability: '8-12%',
        progressWidth: 85
      },
      {
        id: 4,
        title: 'Инвестирование в строительство',
        description: 'По договору подряда с контролем на каждом этапе',
        icon: 'ConstructionIcon',
        features: ['Контроль процесса', 'Высокий потенциал роста', 'Индивидуальный подход'],
        profitability: '15-25%',
        progressWidth: 90
      },
      {
        id: 5,
        title: 'Покупка недвижимости с аукциона',
        description: 'Приобретение объектов по цене ниже рыночной',
        icon: 'AuctionIcon',
        features: ['Низкая цена покупки', 'Высокий потенциал роста', 'Уникальные предложения'],
        profitability: '20-40%',
        progressWidth: 95
      }
    ]
    
    const onTypeHover = (index) => {
      hoveredType.value = index
    }
    
    const onTypeLeave = () => {
      hoveredType.value = null
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
      investmentTypes,
      hoveredType,
      onTypeHover,
      onTypeLeave
    }
  }
}
</script>

<style scoped>
.investment-types {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  position: relative;
  background: linear-gradient(135deg, #1e293b 0%, #334155 50%, #475569 100%);
  padding: var(--spacing-xl) 0;
  overflow: hidden;
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.investment-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.animated-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  opacity: 0.1;
  animation: shapeFloat 20s infinite ease-in-out;
}

.shape-1 {
  width: 100px;
  height: 100px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.3), rgba(255, 215, 0, 0.3));
  border-radius: 50%;
  top: 10%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, rgba(255, 215, 0, 0.3), rgba(216, 4, 42, 0.3));
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
  top: 20%;
  right: 15%;
  animation-delay: 3s;
}

.shape-3 {
  width: 120px;
  height: 120px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.2), rgba(84, 89, 95, 0.2));
  border-radius: 20px;
  bottom: 20%;
  left: 20%;
  animation-delay: 6s;
}

.shape-4 {
  width: 90px;
  height: 90px;
  background: linear-gradient(135deg, rgba(84, 89, 95, 0.3), rgba(216, 4, 42, 0.3));
  clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%);
  bottom: 30%;
  right: 25%;
  animation-delay: 9s;
}

@keyframes shapeFloat {
  0%, 100% { transform: translate(0, 0) rotate(0deg) scale(1); }
  25% { transform: translate(30px, -40px) rotate(90deg) scale(1.1); }
  50% { transform: translate(-20px, -60px) rotate(180deg) scale(0.9); }
  75% { transform: translate(-40px, 30px) rotate(270deg) scale(1.05); }
}

.floating-coins {
  position: absolute;
  width: 100%;
  height: 100%;
}

.coin {
  position: absolute;
  color: rgba(255, 215, 0, 0.4);
  animation: coinFloat 20s infinite linear;
}

@keyframes coinFloat {
  0% { transform: translateY(0) rotate(0deg); opacity: 0; }
  10% { opacity: 1; }
  50% { transform: translateY(-50vh) rotate(180deg); opacity: 0.8; }
  90% { opacity: 1; }
  100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
}

.container {
  position: relative;
  z-index: 2;
}

.section-header {
  margin-bottom: var(--spacing-lg);
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.section-header.visible {
  opacity: 1;
  transform: translateY(0);
}

.section-badge {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  padding: 12px 24px;
  border-radius: 50px;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
  color: white;
  margin-bottom: var(--spacing-lg);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.section-badge svg {
  color: #ffd700;
}

.section-header h2 {
  font-size: clamp(2.5rem, 5vw, 4rem);
  color: white;
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  line-height: 1.2;
}

.highlight {
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.8);
  max-width: 700px;
  margin: 0 auto;
  line-height: 1.6;
}

.investment-content {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: var(--spacing-xl);
  align-items: center;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.investment-content.visible {
  opacity: 1;
  transform: translateY(0);
}

.types-list {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-md);
  max-height: 70vh;
  overflow-y: auto;
}

.type-item {
  position: relative;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: var(--spacing-md);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  opacity: 0;
  transform: translateX(-50px) scale(0.95);
  overflow: hidden;
}

.type-item.visible {
  opacity: 1;
  transform: translateX(0) scale(1);
}

.type-item:hover {
  transform: translateX(15px) scale(1.02);
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.4);
  border-color: rgba(255, 215, 0, 0.5);
  background: rgba(255, 255, 255, 0.15);
}

.type-number {
  position: absolute;
  top: 20px;
  right: 25px;
  font-size: 3.5rem;
  font-weight: var(--font-weight-bold);
  color: rgba(255, 255, 255, 0.1);
  line-height: 1;
  transition: all 0.3s ease;
}

.type-item:hover .type-number {
  color: rgba(255, 215, 0, 0.3);
  transform: scale(1.1);
}

.type-icon {
  position: relative;
  width: 60px;
  height: 60px;
  margin-bottom: var(--spacing-md);
}

.icon-wrapper {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #1e293b;
  transition: all 0.3s ease;
  box-shadow: 0 10px 30px rgba(255, 215, 0, 0.4);
}

.type-item:hover .icon-wrapper {
  transform: rotateY(180deg) scale(1.1);
  box-shadow: 0 15px 40px rgba(255, 215, 0, 0.6);
}

.icon-glow {
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 25px;
  opacity: 0;
  filter: blur(15px);
  transition: opacity 0.3s ease;
  z-index: -1;
}

.type-item:hover .icon-glow {
  opacity: 0.6;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.type-content {
  position: relative;
}

.type-content h3 {
  font-size: 1.2rem;
  color: white;
  margin-bottom: var(--spacing-sm);
  font-weight: var(--font-weight-bold);
  line-height: 1.3;
}

.type-content p {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.5;
  margin-bottom: var(--spacing-md);
  font-size: 0.9rem;
}

.type-features {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: var(--spacing-sm);
}

.feature {
  display: flex;
  align-items: center;
  gap: 6px;
  background: rgba(255, 215, 0, 0.2);
  color: #ffd700;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: var(--font-weight-medium);
  transition: all 0.3s ease;
  border: 1px solid rgba(255, 215, 0, 0.3);
}

.feature:hover {
  background: #ffd700;
  color: #1e293b;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(255, 215, 0, 0.4);
}

.feature svg {
  width: 12px;
  height: 12px;
}

.type-progress {
  margin-top: var(--spacing-md);
}

.progress-label {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
}

.progress-label span:first-child {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
}

.progress-value {
  font-size: 1.1rem;
  font-weight: var(--font-weight-bold);
  color: #ffd700;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 3px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 3px;
  transition: width 1.5s ease 0.5s;
  box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
}

.type-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(255, 215, 0, 0.05) 0%, transparent 50%);
  opacity: 0;
  transition: opacity 0.3s ease;
  border-radius: 25px;
  pointer-events: none;
}

.type-item:hover .type-overlay {
  opacity: 1;
}

.investment-visual {
  position: relative;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.investment-visual.visible {
  opacity: 1;
  transform: translateY(0);
}

.visual-container {
  position: relative;
}

.image-glow {
  position: absolute;
  top: -15px;
  left: -15px;
  right: -15px;
  bottom: -15px;
  background: linear-gradient(135deg, rgba(255, 215, 0, 0.3), rgba(216, 4, 42, 0.3));
  border-radius: 35px;
  filter: blur(30px);
  opacity: 0.7;
  animation: imageGlow 4s ease-in-out infinite alternate;
}

@keyframes imageGlow {
  0% { transform: scale(1); }
  100% { transform: scale(1.05); }
}

.image-wrapper {
  position: relative;
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 0 25px 70px rgba(0, 0, 0, 0.4);
}

.image-wrapper img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.5s ease;
}

.investment-visual:hover .image-wrapper img {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(30, 41, 59, 0.8) 0%, rgba(0, 0, 0, 0.6) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: all 0.3s ease;
}

.investment-visual:hover .image-overlay {
  opacity: 1;
}

.overlay-content {
  text-align: center;
  color: white;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.investment-visual:hover .overlay-content {
  transform: translateY(0);
}

.overlay-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #1e293b;
  margin: 0 auto var(--spacing-md);
  box-shadow: 0 10px 25px rgba(255, 215, 0, 0.4);
}

.overlay-content h3 {
  font-size: 1.5rem;
  margin-bottom: 8px;
  font-weight: var(--font-weight-bold);
}

.overlay-content p {
  font-size: 1rem;
  opacity: 0.9;
}

.floating-stats {
  position: absolute;
  top: 20px;
  right: -20px;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.stat-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 15px;
  padding: 16px;
  display: flex;
  align-items: center;
  gap: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
  animation: statFloat 3s ease-in-out infinite alternate;
}

.stat-card:nth-child(2) {
  animation-delay: 1s;
}

@keyframes statFloat {
  0% { transform: translateY(0); }
  100% { transform: translateY(-10px); }
}

.stat-icon {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #1e293b;
}

.stat-text {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-size: 1.3rem;
  font-weight: var(--font-weight-bold);
  color: white;
  line-height: 1;
}

.stat-label {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.7);
}

@media (max-width: 1200px) {
  .investment-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-2xl);
  }
  
  .floating-stats {
    position: relative;
    top: auto;
    right: auto;
    flex-direction: row;
    justify-content: center;
    margin-top: var(--spacing-lg);
  }
}

@media (max-width: 768px) {
  .investment-types {
    padding: var(--spacing-2xl) 0;
  }
  
  .type-item {
    padding: var(--spacing-lg);
  }
  
  .type-item:hover {
    transform: translateY(-10px) scale(1.02);
  }
  
  .floating-stats {
    flex-direction: column;
    align-items: center;
  }
  
  .stat-card {
    width: 100%;
    max-width: 200px;
  }
}
</style>