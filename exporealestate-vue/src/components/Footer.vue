<template>
  <footer class="footer full-width" ref="footerRef">
    <div class="footer-background">
      <div class="footer-pattern">
        <div class="pattern-grid" v-for="n in 12" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               top: Math.random() * 100 + '%',
               animationDelay: Math.random() * 4 + 's'
             }">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
            <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="1" fill="none"/>
          </svg>
        </div>
      </div>
      <div class="footer-glow"></div>
    </div>

    <div class="container">
      <div class="footer-content" :class="{ visible: isVisible }">
        <div class="footer-brand">
          <div class="brand-logo">
            <div class="logo-icon">
              <svg width="50" height="50" viewBox="0 0 24 24" fill="none">
                <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
              </svg>
            </div>
            <div class="brand-text">
              <h3>EXPO REAL ESTATE</h3>
              <p>Международная выставка недвижимости</p>
            </div>
          </div>
          <div class="social-links">
            <a href="#" class="social-link" @mouseenter="onSocialHover" @mouseleave="onSocialLeave">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M7 10v4h3v7h4v-7h3l1-4h-4V8a1 1 0 0 1 1-1h3V3h-3a5 5 0 0 0-5 5v2H7z" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </a>
            <a href="#" class="social-link" @mouseenter="onSocialHover" @mouseleave="onSocialLeave">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <rect width="20" height="20" x="2" y="2" rx="5" ry="5" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z" stroke="currentColor" stroke-width="2" fill="none"/>
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
              </svg>
            </a>
            <a href="#" class="social-link" @mouseenter="onSocialHover" @mouseleave="onSocialLeave">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M22.46 6c-.77.35-1.6.58-2.46.69.88-.53 1.56-1.37 1.88-2.38-.83.5-1.75.85-2.72 1.05C18.37 4.5 17.26 4 16 4c-2.35 0-4.27 1.92-4.27 4.29 0 .34.04.67.11.98C8.28 9.09 5.11 7.38 3 4.79c-.37.63-.58 1.37-.58 2.15 0 1.49.75 2.81 1.91 3.56-.71 0-1.37-.2-1.95-.5v.03c0 2.08 1.48 3.82 3.44 4.21a4.22 4.22 0 0 1-1.93.07 4.28 4.28 0 0 0 4 2.98 8.521 8.521 0 0 1-5.33 1.84c-.34 0-.68-.02-1.02-.06C3.44 20.29 5.7 21 8.12 21 16 21 20.33 14.46 20.33 8.79c0-.19 0-.37-.01-.56.84-.6 1.56-1.36 2.14-2.23z" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </a>
            <a href="#" class="social-link" @mouseenter="onSocialHover" @mouseleave="onSocialLeave">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z" stroke="currentColor" stroke-width="2" fill="none"/>
                <rect width="4" height="12" x="2" y="9" stroke="currentColor" stroke-width="2" fill="none"/>
                <circle cx="4" cy="4" r="2" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </a>
          </div>
        </div>

        <div class="footer-info">
          <div class="info-section">
            <div class="section-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z" stroke="currentColor" stroke-width="2" fill="none"/>
                <circle cx="12" cy="10" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </div>
            <div class="section-content">
              <h4>Наш офис</h4>
              <p>Деловой Центр Москва-Сити<br>Пресненская набережная, 2<br>Москва, Россия</p>
            </div>
          </div>

          <div class="info-section">
            <div class="section-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z" stroke="currentColor" stroke-width="2" fill="none"/>
                <polyline points="22,6 12,13 2,6" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </div>
            <div class="section-content">
              <h4>Email</h4>
              <a href="mailto:org@exporealestate.ru" class="contact-link">org@exporealestate.ru</a>
            </div>
          </div>

          <div class="info-section">
            <div class="section-icon">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </div>
            <div class="section-content">
              <h4>Телефон</h4>
              <a href="tel:+74993500006" class="contact-link">+7 (499) 350-00-06</a>
            </div>
          </div>
        </div>

        <div class="footer-map">
          <div class="map-header">
            <div class="map-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
            </div>
            <h4>Как добраться</h4>
          </div>
          <div class="map-container">
            <div class="map-placeholder">
              <div class="map-pin">
                <svg width="40" height="40" viewBox="0 0 24 24" fill="none">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z" stroke="currentColor" stroke-width="2" fill="none"/>
                  <circle cx="12" cy="10" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
                </svg>
              </div>
              <div class="map-info">
                <p>Москва-Сити</p>
                <p>Башня Федерация</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="footer-exhibition" :class="{ visible: isVisible }">
        <div class="exhibition-background">
          <div class="exhibition-glow"></div>
        </div>
        <div class="exhibition-content">
          <div class="exhibition-icon">
            <svg width="60" height="60" viewBox="0 0 24 24" fill="none">
              <path d="M12 2L3.09 8.26L4 21L20 21L20.91 8.26L12 2Z" stroke="currentColor" stroke-width="2" fill="none"/>
              <path d="M12 7L8 10.5V17H16V10.5L12 7Z" fill="currentColor"/>
              <circle cx="12" cy="12" r="2" stroke="white" stroke-width="2" fill="white"/>
            </svg>
          </div>
          <div class="exhibition-info">
            <h3>Выставка Show-Room</h3>
            <p>Посетите нашу выставку недвижимости в самом сердце делового центра Москвы. Современные технологии презентации, VR-туры и персональные консультации.</p>
            <div class="exhibition-features">
              <div class="feature">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                  <path d="M9 12l2 2 4-4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                </svg>
                <span>VR-презентации</span>
              </div>
              <div class="feature">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                  <path d="M9 12l2 2 4-4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                </svg>
                <span>Персональные консультации</span>
              </div>
              <div class="feature">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                  <path d="M9 12l2 2 4-4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/>
                </svg>
                <span>Интерактивные модели</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      
    </div>
    
    <div class="footer-bottom full-width" :class="{ visible: isVisible }">
      <div class="container">
        <div class="footer-bottom-content">
          <div class="footer-copyright">
            <p>&copy; 2025 EXPO REAL ESTATE. Все права защищены.</p>
            <p>Международная выставка недвижимости премиум-класса</p>
          </div>
          <div class="footer-links">
            <a href="#privacy" class="footer-link">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                <rect width="18" height="11" x="3" y="11" rx="2" ry="2" stroke="currentColor" stroke-width="2" fill="none"/>
                <circle cx="12" cy="16" r="1" stroke="currentColor" stroke-width="2" fill="none"/>
                <path d="M7 11V7a5 5 0 0 1 10 0v4" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
              Политика конфиденциальности
            </a>
            <a href="#terms" class="footer-link">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z" stroke="currentColor" stroke-width="2" fill="none"/>
                <polyline points="14,2 14,8 20,8" stroke="currentColor" stroke-width="2" fill="none"/>
                <line x1="16" y1="13" x2="8" y2="13" stroke="currentColor" stroke-width="2"/>
                <line x1="16" y1="17" x2="8" y2="17" stroke="currentColor" stroke-width="2"/>
                <polyline points="10,9 9,9 8,9" stroke="currentColor" stroke-width="2" fill="none"/>
              </svg>
              Пользовательское соглашение
            </a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'Footer',
  setup() {
    const footerRef = ref(null)
    const isVisible = ref(false)
    
    const onSocialHover = (event) => {
      event.currentTarget.style.transform = 'translateY(-5px) rotate(5deg) scale(1.1)'
    }
    
    const onSocialLeave = (event) => {
      event.currentTarget.style.transform = 'translateY(0) rotate(0deg) scale(1)'
    }
    
    const observeSection = () => {
      const observer = new IntersectionObserver(
        ([entry]) => {
          isVisible.value = entry.isIntersecting
        },
        { threshold: 0.1 }
      )
      
      if (footerRef.value) {
        observer.observe(footerRef.value)
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
      footerRef,
      isVisible,
      onSocialHover,
      onSocialLeave
    }
  }
}
</script>

<style scoped>
.footer {
  position: relative;
  background: linear-gradient(135deg, #0f1419 0%, #1a1f2e 50%, #0f1419 100%);
  color: white;
  overflow: hidden;
  margin: 0;
}

.footer-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.footer-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.pattern-grid {
  position: absolute;
  color: rgba(216, 4, 42, 0.03);
  animation: floatPattern 12s ease-in-out infinite;
}

@keyframes floatPattern {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
    opacity: 0.3;
  }
  25% {
    transform: translateY(-20px) rotate(90deg);
    opacity: 0.1;
  }
  50% {
    transform: translateY(-10px) rotate(180deg);
    opacity: 0.2;
  }
  75% {
    transform: translateY(-30px) rotate(270deg);
    opacity: 0.15;
  }
}

.footer-glow {
  position: absolute;
  top: 0;
  left: 50%;
  width: 1000px;
  height: 300px;
  background: radial-gradient(ellipse, rgba(216, 4, 42, 0.08) 0%, transparent 70%);
  transform: translateX(-50%);
  animation: glowPulse 10s ease-in-out infinite;
}

@keyframes glowPulse {
  0%, 100% {
    transform: translateX(-50%) scale(1);
    opacity: 0.4;
  }
  50% {
    transform: translateX(-50%) scale(1.3);
    opacity: 0.7;
  }
}

.footer-content {
  display: grid;
  grid-template-columns: 1fr 1.2fr 1fr;
  gap: var(--spacing-xl);
  margin-bottom: var(--spacing-3xl);
  position: relative;
  z-index: 2;
  transform: translateY(30px);
  opacity: 0;
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.footer-content.visible {
  transform: translateY(0);
  opacity: 1;
}

.footer-brand {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.brand-logo {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: var(--spacing-md);
}

.logo-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 70px;
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 20px;
  color: white;
  box-shadow: 0 10px 40px rgba(216, 4, 42, 0.3);
  position: relative;
  overflow: hidden;
}

.logo-icon::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: conic-gradient(from 0deg at 50% 50%, rgba(255,255,255,0.1) 0deg, transparent 60deg, rgba(255,255,255,0.1) 120deg, transparent 180deg);
  animation: rotateConic 4s linear infinite;
}

@keyframes rotateConic {
  to { transform: rotate(360deg); }
}

.brand-text h3 {
  font-size: 1.5rem;
  font-weight: var(--font-weight-bold);
  color: white;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, #ffffff 0%, var(--color-primary) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.brand-text p {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  color: rgba(255, 255, 255, 0.7);
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  backdrop-filter: blur(20px);
  position: relative;
  overflow: hidden;
}

.social-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(216, 4, 42, 0.2), transparent);
  transition: left 0.5s;
}

.social-link:hover::before {
  left: 100%;
}

.social-link:hover {
  background: rgba(216, 4, 42, 0.1);
  border-color: var(--color-primary);
  color: var(--color-primary);
  box-shadow: 0 10px 30px rgba(216, 4, 42, 0.2);
}

.footer-info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.info-section {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1.5rem;
  background: rgba(255, 255, 255, 0.03);
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  transition: var(--transition);
  position: relative;
  overflow: hidden;
}

.info-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(216, 4, 42, 0.05), transparent);
  transition: left 0.6s;
}

.info-section:hover::before {
  left: 100%;
}

.info-section:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(216, 4, 42, 0.2);
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.section-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 12px;
  color: white;
  flex-shrink: 0;
  box-shadow: 0 5px 20px rgba(216, 4, 42, 0.3);
}

.section-content h4 {
  font-size: 1.1rem;
  font-weight: var(--font-weight-semibold);
  color: white;
  margin-bottom: 0.5rem;
}

.section-content p {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  line-height: 1.5;
}

.contact-link {
  color: var(--color-primary);
  font-weight: var(--font-weight-medium);
  transition: var(--transition);
}

.contact-link:hover {
  color: #e91e63;
  text-decoration: underline;
}

.footer-map {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.map-header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.map-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 10px;
  color: white;
}

.map-header h4 {
  font-size: 1.2rem;
  font-weight: var(--font-weight-semibold);
  color: white;
}

.map-container {
  position: relative;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  backdrop-filter: blur(20px);
  transition: var(--transition);
}

.map-container:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(216, 4, 42, 0.2);
  transform: translateY(-2px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
}

.map-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 1rem;
}

.map-pin {
  color: var(--color-primary);
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.map-info p {
  color: rgba(255, 255, 255, 0.8);
  font-size: 0.9rem;
  margin: 0;
}

.map-info p:first-child {
  font-weight: var(--font-weight-semibold);
  color: white;
}

.footer-exhibition {
  position: relative;
  background: linear-gradient(135deg, rgba(216, 4, 42, 0.1) 0%, rgba(233, 30, 99, 0.1) 100%);
  border: 1px solid rgba(216, 4, 42, 0.2);
  border-radius: 25px;
  padding: var(--spacing-xl);
  margin-bottom: var(--spacing-xl);
  backdrop-filter: blur(20px);
  overflow: hidden;
  transform: translateY(30px);
  opacity: 0;
  transition: all 1s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.3s;
}

.footer-exhibition.visible {
  transform: translateY(0);
  opacity: 1;
}

.exhibition-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.exhibition-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 200%;
  height: 150%;
  background: radial-gradient(ellipse, rgba(216, 4, 42, 0.1) 0%, transparent 70%);
  transform: translate(-50%, -50%);
  animation: exhibitionGlow 8s ease-in-out infinite;
}

@keyframes exhibitionGlow {
  0%, 100% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 0.5;
  }
  50% {
    transform: translate(-50%, -50%) scale(1.2);
    opacity: 0.8;
  }
}

.exhibition-content {
  position: relative;
  z-index: 2;
  display: flex;
  align-items: flex-start;
  gap: var(--spacing-lg);
}

.exhibition-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 100px;
  background: linear-gradient(135deg, var(--color-primary) 0%, #e91e63 100%);
  border-radius: 25px;
  color: white;
  flex-shrink: 0;
  box-shadow: 0 20px 50px rgba(216, 4, 42, 0.3);
  position: relative;
  overflow: hidden;
}

.exhibition-icon::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: conic-gradient(from 0deg at 50% 50%, rgba(255,255,255,0.2) 0deg, transparent 60deg, rgba(255,255,255,0.2) 120deg, transparent 180deg);
  animation: rotateConic 6s linear infinite;
}

.exhibition-info h3 {
  font-size: 2rem;
  font-weight: var(--font-weight-bold);
  color: white;
  margin-bottom: var(--spacing-md);
  background: linear-gradient(135deg, #ffffff 0%, var(--color-primary) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.exhibition-info p {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: var(--spacing-lg);
}

.exhibition-features {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.feature {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: rgba(255, 255, 255, 0.9);
  font-size: 0.9rem;
}

.feature svg {
  color: var(--color-primary);
  flex-shrink: 0;
}

.footer-bottom {
  position: relative;
  z-index: 2;
  padding: var(--spacing-lg) 0;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(20px);
  transform: translateY(20px);
  opacity: 0;
  transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) 0.5s;
  margin: 0;
}

.footer-bottom.visible {
  transform: translateY(0);
  opacity: 1;
}

.footer-bottom-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: var(--spacing-lg);
}

.footer-copyright {
  flex: 1;
}

.footer-copyright p {
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
  margin: 0.25rem 0;
}

.footer-copyright p:first-child {
  color: rgba(255, 255, 255, 0.8);
  font-weight: var(--font-weight-medium);
}

.footer-links {
  display: flex;
  gap: var(--spacing-lg);
}

.footer-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  transition: var(--transition);
  backdrop-filter: blur(20px);
}

.footer-link:hover {
  background: rgba(216, 4, 42, 0.1);
  border-color: var(--color-primary);
  color: var(--color-primary);
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(216, 4, 42, 0.2);
}

@media (max-width: 1024px) {
  .footer-content {
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-lg);
  }
  
  .footer-map {
    grid-column: 1 / -1;
    margin-top: var(--spacing-lg);
  }
  
  .exhibition-content {
    flex-direction: column;
    text-align: center;
  }
  
  .exhibition-icon {
    align-self: center;
  }
}

@media (max-width: 768px) {
  .footer {
    padding: var(--spacing-xl) 0 0;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    gap: var(--spacing-lg);
  }
  
  .brand-logo {
    justify-content: center;
    text-align: center;
  }
  
  .social-links {
    justify-content: center;
  }
  
  .footer-exhibition {
    padding: var(--spacing-lg);
  }
  
  .exhibition-info h3 {
    font-size: 1.5rem;
  }
  
  .footer-bottom-content {
    flex-direction: column;
    text-align: center;
    gap: var(--spacing-md);
  }
  
  .footer-links {
    flex-direction: column;
    gap: var(--spacing-sm);
  }
}

@media (max-width: 480px) {
  .info-section {
    padding: 1rem;
  }
  
  .section-icon {
    width: 40px;
    height: 40px;
  }
  
  .exhibition-icon {
    width: 80px;
    height: 80px;
  }
  
  .exhibition-info h3 {
    font-size: 1.3rem;
  }
  
  .social-links {
    flex-wrap: wrap;
    gap: 0.75rem;
  }
  
  .social-link {
    width: 45px;
    height: 45px;
  }
}
</style>