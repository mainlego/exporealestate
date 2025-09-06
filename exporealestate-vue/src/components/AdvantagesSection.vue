<template>
  <section class="advantages section full-width" ref="sectionRef">
    <div class="advantages-background">
      <div class="floating-elements">
        <div class="floating-element" v-for="n in 20" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               top: Math.random() * 100 + '%',
               animationDelay: Math.random() * 10 + 's',
               animationDuration: (15 + Math.random() * 10) + 's'
             }"></div>
      </div>
      <div class="gradient-orbs">
        <div class="gradient-orb gradient-orb-1"></div>
        <div class="gradient-orb gradient-orb-2"></div>
        <div class="gradient-orb gradient-orb-3"></div>
      </div>
    </div>

    <div class="container">
      <div class="section-header text-center" :class="{ visible: isVisible }">
        <div class="section-badge">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
            <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
          </svg>
          Ваши преимущества
        </div>
        <h2>Эксклюзивные возможности<br><span class="highlight">для инвесторов</span></h2>
        <p class="section-subtitle">Откройте для себя уникальные преимущества участия в выставке недвижимости</p>
      </div>
      
      <div class="advantages-grid">
        <div 
          class="advantage-card" 
          v-for="(advantage, index) in advantages" 
          :key="advantage.id"
          :class="{ visible: isVisible }"
          :style="{ animationDelay: (index * 0.2) + 's' }"
          @mouseenter="onCardHover(index)"
          @mouseleave="onCardLeave(index)"
        >
          <div class="advantage-number">{{ String(advantage.id).padStart(2, '0') }}</div>
          <div class="advantage-icon">
            <div class="icon-wrapper">
              <component :is="advantage.icon" />
            </div>
            <div class="icon-glow"></div>
          </div>
          <div class="advantage-content">
            <h3>{{ advantage.title }}</h3>
            <p>{{ advantage.description }}</p>
            <div class="advantage-features" v-if="advantage.features">
              <div v-for="feature in advantage.features" :key="feature" class="feature">
                <svg width="12" height="12" viewBox="0 0 24 24" fill="none">
                  <path d="M20 6L9 17l-5-5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
                {{ feature }}
              </div>
            </div>
            <div class="card-overlay"></div>
          </div>
        </div>
      </div>
      
      <div class="conference-section" :class="{ visible: isVisible }">
        <div class="conference-background">
          <div class="conference-pattern"></div>
        </div>
        <div class="conference-content">
          <div class="conference-text">
            <div class="conference-icon">
              <svg width="60" height="60" viewBox="0 0 24 24" fill="none">
                <rect x="2" y="3" width="20" height="14" rx="2" ry="2" stroke="currentColor" stroke-width="2" fill="none"/>
                <line x1="8" y1="21" x2="16" y2="21" stroke="currentColor" stroke-width="2"/>
                <line x1="12" y1="17" x2="12" y2="21" stroke="currentColor" stroke-width="2"/>
                <circle cx="7" cy="8" r="2" fill="currentColor"/>
                <circle cx="12" cy="8" r="2" fill="currentColor"/>
                <circle cx="17" cy="8" r="2" fill="currentColor"/>
              </svg>
            </div>
            <h2>Деловая конференция</h2>
            <p>
              В течение всех дней выставки вы сможете посетить деловую программу, 
              послушать лучших экспертов в области инвестиций в недвижимость, 
              узнать о трендах и тенденциях в отрасли, получить ценные советы от 
              ТОПовых мировых представителей и завязать деловые контакты.
            </p>
            <div class="conference-stats">
              <div class="stat">
                <span class="stat-number">50+</span>
                <span class="stat-label">Экспертов</span>
              </div>
              <div class="stat">
                <span class="stat-number">15+</span>
                <span class="stat-label">Докладов</span>
              </div>
              <div class="stat">
                <span class="stat-number">3</span>
                <span class="stat-label">Дня</span>
              </div>
            </div>
          </div>
          
          <div class="prize-section">
            <div class="prize-container">
              <div class="prize-glow"></div>
              <div class="prize-image">
                <img src="/assets/images/rozygrysh-avto.png" alt="Розыгрыш автомобиля" />
                <div class="prize-shimmer"></div>
              </div>
              <div class="prize-text">
                <div class="prize-icon">
                  <svg width="40" height="40" viewBox="0 0 24 24" fill="none">
                    <path d="M12 2L15.09 8.26L22 9L17 14L18.18 21L12 17.77L5.82 21L7 14L2 9L8.91 8.26L12 2Z" 
                          fill="currentColor" stroke="currentColor" stroke-width="2"/>
                  </svg>
                </div>
                <h3>Розыгрыш призов</h3>
                <p>Не упустите шанс выиграть ценные призы на нашей выставке</p>
                <div class="prize-cta">
                  <span>Участвуйте бесплатно</span>
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                    <path d="M5 12h14M12 5l7 7-7 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
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

const DiamondIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M6 9L12 3L18 9L12 21L6 9Z" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M6 9H18" stroke="currentColor" stroke-width="2"/>
      <path d="M9 3L12 9L15 3" stroke="currentColor" stroke-width="2" fill="none"/>
    </svg>
  `
}

const HandshakeIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M11 17a4 4 0 0 1-8 0V5a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v12zM13 7a4 4 0 0 1 8 0v10a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2V7z" fill="currentColor"/>
    </svg>
  `
}

const ShieldIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z" stroke="currentColor" stroke-width="2" fill="none"/>
      <path d="M9 12l2 2 4-4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  `
}

const UserIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      <circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
    </svg>
  `
}

const ClockIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
      <polyline points="12,6 12,12 16,14" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  `
}

const TrendingUpIcon = {
  template: `
    <svg width="48" height="48" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <polyline points="23,6 13.5,15.5 8.5,10.5 1,18" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
      <polyline points="17,6 23,6 23,12" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  `
}

export default {
  name: 'AdvantagesSection',
  components: {
    DiamondIcon,
    HandshakeIcon,
    ShieldIcon,
    UserIcon,
    ClockIcon,
    TrendingUpIcon
  },
  setup() {
    const sectionRef = ref(null)
    const isVisible = ref(false)
    const hoveredCard = ref(null)
    
    const advantages = [
      {
        id: 1,
        title: 'Эксклюзивные предложения',
        description: 'Вы будете первыми кто сможет ознакомиться с самыми интересными предложениями на рынке зарубежной недвижимости и стать инвестором в перспективном проекте.',
        icon: 'DiamondIcon',
        features: ['VIP участники', 'Закрытые предложения', 'Международные партнеры']
      },
      {
        id: 2,
        title: 'Переговоры с первыми лицами',
        description: 'На выставке вы напрямую обсудите и получите выгодные предложения от представителей компаний по инвестиционным доходам, способам инвестирования, возможным рискам.',
        icon: 'HandshakeIcon',
        features: ['Прямой контакт', 'Персональные встречи', 'Гарантии']
      },
      {
        id: 3,
        title: 'Приватность',
        description: 'Уникальный формат выставки show room позволяет проводить переговоры с экспонентами и партнерами выставки в специально отведенных переговорных комнатах.',
        icon: 'ShieldIcon',
        features: ['Конфиденциальность', 'VIP зоны', 'Персональный сервис']
      },
      {
        id: 4,
        title: 'Индивидуальный подбор',
        description: 'Выставка show-room предоставляет своим посетителям возможность зарезервировать VIP переговорную с персональным менеджером.',
        icon: 'UserIcon',
        features: ['Персональный подход', 'Экспертная консультация', 'Индивидуальные решения']
      },
      {
        id: 5,
        title: 'Экономия времени и ресурсов',
        description: 'Вы сможете побывать за рубежом не покидая город и ознакомиться с предложениями об инвестициях сразу в нескольких странах.',
        icon: 'ClockIcon',
        features: ['Время - деньги', 'Все в одном месте', 'Без командировок']
      },
      {
        id: 6,
        title: 'Выгодные условия покупки',
        description: 'Многие экспоненты предлагают гостям выставки специальные условия покупки зарубежной недвижимости и эксклюзивные банковские предложения.',
        icon: 'TrendingUpIcon',
        features: ['Специальные цены', 'Банковские продукты', 'Льготные условия']
      }
    ]
    
    const onCardHover = (index) => {
      hoveredCard.value = index
    }
    
    const onCardLeave = () => {
      hoveredCard.value = null
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
      advantages,
      hoveredCard,
      onCardHover,
      onCardLeave
    }
  }
}
</script>

<style scoped>
.advantages {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  position: relative;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 50%, #cbd5e1 100%);
  padding: var(--spacing-3xl) 0;
  overflow: hidden;
}

.advantages-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.floating-elements {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.floating-element {
  position: absolute;
  width: 6px;
  height: 6px;
  background: rgba(216, 4, 42, 0.3);
  border-radius: 50%;
  animation: float 20s infinite ease-in-out;
}

@keyframes float {
  0%, 100% { transform: translateY(0) rotate(0deg); opacity: 0; }
  10% { opacity: 1; }
  50% { transform: translateY(-100vh) rotate(180deg); opacity: 0.6; }
  90% { opacity: 1; }
}

.gradient-orbs {
  position: absolute;
  width: 100%;
  height: 100%;
}

.gradient-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(60px);
  animation: orbFloat 15s infinite ease-in-out;
}

.gradient-orb-1 {
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, rgba(216, 4, 42, 0.1) 0%, rgba(216, 4, 42, 0.05) 50%, transparent 70%);
  top: -200px;
  left: -200px;
  animation-delay: 0s;
}

.gradient-orb-2 {
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, rgba(84, 89, 95, 0.08) 0%, rgba(84, 89, 95, 0.04) 50%, transparent 70%);
  top: 50%;
  right: -150px;
  animation-delay: 5s;
}

.gradient-orb-3 {
  width: 250px;
  height: 250px;
  background: radial-gradient(circle, rgba(216, 4, 42, 0.06) 0%, rgba(216, 4, 42, 0.03) 50%, transparent 70%);
  bottom: -125px;
  left: 50%;
  animation-delay: 10s;
}

@keyframes orbFloat {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(50px, -30px) scale(1.1); }
  66% { transform: translate(-30px, 50px) scale(0.9); }
}

.container {
  position: relative;
  z-index: 2;
}

.section-header {
  margin-bottom: var(--spacing-3xl);
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

.section-header h2 {
  font-size: clamp(2.5rem, 5vw, 4rem);
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  line-height: 1.2;
}

.highlight {
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.2rem;
  color: var(--color-secondary);
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.advantages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-3xl);
}

.advantage-card {
  position: relative;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 25px;
  padding: var(--spacing-xl);
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.08);
  border: 1px solid rgba(216, 4, 42, 0.1);
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  opacity: 0;
  transform: translateY(50px) scale(0.95);
  overflow: hidden;
}

.advantage-card.visible {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.advantage-card:hover {
  transform: translateY(-15px) scale(1.02);
  box-shadow: 0 30px 80px rgba(216, 4, 42, 0.15);
  border-color: var(--color-primary);
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
  position: relative;
  width: 80px;
  height: 80px;
  margin-bottom: var(--spacing-lg);
}

.icon-wrapper {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  transition: all 0.3s ease;
  box-shadow: 0 10px 30px rgba(216, 4, 42, 0.3);
}

.advantage-card:hover .icon-wrapper {
  transform: rotateY(180deg) scale(1.1);
  box-shadow: 0 15px 40px rgba(216, 4, 42, 0.4);
}

.icon-glow {
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  border-radius: 25px;
  opacity: 0;
  filter: blur(15px);
  transition: opacity 0.3s ease;
  z-index: -1;
}

.advantage-card:hover .icon-glow {
  opacity: 0.5;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.advantage-content {
  position: relative;
}

.advantage-content h3 {
  font-size: 1.6rem;
  color: var(--color-text);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
  line-height: 1.3;
}

.advantage-content p {
  color: var(--color-secondary);
  line-height: 1.7;
  margin-bottom: var(--spacing-lg);
  font-size: 1rem;
}

.advantage-features {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.feature {
  display: flex;
  align-items: center;
  gap: 6px;
  background: rgba(216, 4, 42, 0.1);
  color: var(--color-primary);
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: var(--font-weight-medium);
  transition: all 0.3s ease;
  border: 1px solid rgba(216, 4, 42, 0.2);
}

.feature:hover {
  background: var(--color-primary);
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(216, 4, 42, 0.3);
}

.feature svg {
  width: 12px;
  height: 12px;
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.05) 0%, transparent 50%);
  opacity: 0;
  transition: opacity 0.3s ease;
  border-radius: 25px;
  pointer-events: none;
}

.advantage-card:hover .card-overlay {
  opacity: 1;
}

.conference-section {
  position: relative;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(20px);
  border-radius: 30px;
  padding: var(--spacing-3xl);
  border: 1px solid rgba(216, 4, 42, 0.1);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.08);
  overflow: hidden;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.conference-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.conference-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  opacity: 0.03;
}

.conference-pattern {
  width: 100%;
  height: 100%;
  background-image: radial-gradient(circle at 25px 25px, rgba(216, 4, 42, 0.3) 2px, transparent 2px);
  background-size: 50px 50px;
  animation: patternMove 20s linear infinite;
}

@keyframes patternMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

.conference-content {
  position: relative;
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: var(--spacing-3xl);
  align-items: center;
}

.conference-text {
  position: relative;
}

.conference-icon {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  margin-bottom: var(--spacing-lg);
  box-shadow: 0 10px 30px rgba(216, 4, 42, 0.3);
}

.conference-text h2 {
  font-size: clamp(2rem, 4vw, 3rem);
  color: var(--color-text);
  margin-bottom: var(--spacing-lg);
  font-weight: var(--font-weight-bold);
}

.conference-text p {
  font-size: 1.1rem;
  color: var(--color-secondary);
  line-height: 1.7;
  margin-bottom: var(--spacing-xl);
}

.conference-stats {
  display: flex;
  gap: var(--spacing-lg);
}

.stat {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: var(--font-weight-bold);
  color: var(--color-primary);
  line-height: 1;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--color-secondary);
  font-weight: var(--font-weight-medium);
}

.prize-section {
  text-align: center;
}

.prize-container {
  position: relative;
}

.prize-glow {
  position: absolute;
  top: -10px;
  left: -10px;
  right: -10px;
  bottom: -10px;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.2), rgba(255, 215, 0, 0.2));
  border-radius: 25px;
  filter: blur(20px);
  opacity: 0.7;
  animation: prizeGlow 3s ease-in-out infinite alternate;
}

@keyframes prizeGlow {
  0% { transform: scale(1); }
  100% { transform: scale(1.05); }
}

.prize-image {
  position: relative;
  margin-bottom: var(--spacing-lg);
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
}

.prize-image img {
  max-width: 100%;
  height: auto;
  display: block;
}

.prize-shimmer {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  animation: shimmer 3s infinite;
}

@keyframes shimmer {
  0% { left: -100%; }
  100% { left: 100%; }
}

.prize-text {
  position: relative;
}

.prize-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  margin: 0 auto var(--spacing-md);
  box-shadow: 0 10px 25px rgba(255, 215, 0, 0.4);
  animation: starPulse 2s ease-in-out infinite;
}

@keyframes starPulse {
  0%, 100% { transform: scale(1) rotate(0deg); }
  50% { transform: scale(1.1) rotate(5deg); }
}

.prize-text h3 {
  font-size: 2.2rem;
  color: var(--color-primary);
  margin-bottom: var(--spacing-md);
  font-weight: var(--font-weight-bold);
}

.prize-text p {
  font-size: 1.1rem;
  color: var(--color-secondary);
  line-height: 1.6;
  margin-bottom: var(--spacing-lg);
}

.prize-cta {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  color: white;
  padding: 12px 24px;
  border-radius: 50px;
  font-weight: var(--font-weight-medium);
  box-shadow: 0 10px 25px rgba(216, 4, 42, 0.3);
  transition: all 0.3s ease;
}

.prize-cta:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 35px rgba(216, 4, 42, 0.4);
}

.prize-cta svg {
  transition: transform 0.3s ease;
}

.prize-cta:hover svg {
  transform: translateX(3px);
}

@media (max-width: 1200px) {
  .advantages-grid {
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  }
  
  .conference-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-2xl);
    text-align: center;
  }
}

@media (max-width: 768px) {
  .advantages {
    padding: var(--spacing-2xl) 0;
  }
  
  .advantages-grid {
    grid-template-columns: 1fr;
    gap: var(--spacing-lg);
  }
  
  .advantage-card {
    padding: var(--spacing-lg);
  }
  
  .conference-section {
    padding: var(--spacing-2xl);
  }
  
  .conference-stats {
    justify-content: center;
    flex-wrap: wrap;
  }
}
</style>