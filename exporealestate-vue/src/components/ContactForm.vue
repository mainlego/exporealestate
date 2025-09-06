<template>
  <section class="contact-form section full-width" ref="sectionRef">
    <div class="contact-background">
      <div class="animated-grid">
        <div class="grid-line" v-for="n in 20" :key="n" 
             :style="{ 
               left: (n * 5) + '%', 
               animationDelay: (n * 0.1) + 's',
               animationDuration: (8 + Math.random() * 4) + 's'
             }"></div>
      </div>
      <div class="floating-envelopes">
        <div class="envelope" v-for="n in 6" :key="n" 
             :style="{ 
               left: Math.random() * 100 + '%', 
               top: Math.random() * 100 + '%',
               animationDelay: Math.random() * 5 + 's',
               animationDuration: (15 + Math.random() * 5) + 's'
             }">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z" stroke="currentColor" stroke-width="2" fill="none"/>
            <polyline points="22,6 12,13 2,6" stroke="currentColor" stroke-width="2" fill="none"/>
          </svg>
        </div>
      </div>
      <div class="contact-glow"></div>
    </div>

    <div class="container">
      <div class="section-header text-center" :class="{ visible: isVisible }">
        <div class="section-badge">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z" stroke="currentColor" stroke-width="2" fill="none"/>
            <polyline points="22,6 12,13 2,6" stroke="currentColor" stroke-width="2" fill="none"/>
          </svg>
          Связь с нами
        </div>
        <h2>Получите консультацию<br><span class="highlight">экспертов</span></h2>
        <p class="section-subtitle">Оставьте заявку и мы проконсультируем вас по всем вопросам инвестиций</p>
      </div>
      
      <div class="form-container" :class="{ visible: isVisible }">
        <div class="form-visual">
          <div class="visual-container">
            <div class="image-frame">
              <div class="frame-decoration"></div>
              <div class="image-wrapper">
                <img src="/assets/images/свяжитесь_с_нами_фото_здания.jpg" alt="Свяжитесь с нами" />
                <div class="image-overlay">
                  <div class="overlay-content">
                    <div class="overlay-icon">
                      <svg width="60" height="60" viewBox="0 0 24 24" fill="none">
                        <path d="M22 12h-4l-3 9L9 3l-3 9H2" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                      </svg>
                    </div>
                    <h3>Мы на связи 24/7</h3>
                    <p>Профессиональная поддержка</p>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="contact-info">
              <div class="info-card">
                <div class="info-icon">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                    <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z" stroke="currentColor" stroke-width="2" fill="none"/>
                  </svg>
                </div>
                <div class="info-text">
                  <span class="info-label">Телефон</span>
                  <span class="info-value">+7 (495) 123-45-67</span>
                </div>
              </div>
              <div class="info-card">
                <div class="info-icon">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                    <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z" stroke="currentColor" stroke-width="2" fill="none"/>
                    <polyline points="22,6 12,13 2,6" stroke="currentColor" stroke-width="2" fill="none"/>
                  </svg>
                </div>
                <div class="info-text">
                  <span class="info-label">Email</span>
                  <span class="info-value">info@exporealestate.ru</span>
                </div>
              </div>
              <div class="info-card">
                <div class="info-icon">
                  <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                    <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z" stroke="currentColor" stroke-width="2" fill="none"/>
                    <circle cx="12" cy="10" r="3" stroke="currentColor" stroke-width="2" fill="none"/>
                  </svg>
                </div>
                <div class="info-text">
                  <span class="info-label">Адрес</span>
                  <span class="info-value">Москва-Сити</span>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="form-content">
          <div class="form-wrapper">
            <div class="form-background">
              <div class="form-pattern"></div>
            </div>
            
            <form @submit.prevent="submitForm" class="contact-form-wrapper" :class="{ submitting: isSubmitting }">
              <div class="form-steps">
                <div class="step" :class="{ active: currentStep >= 1 }">1</div>
                <div class="step-line"></div>
                <div class="step" :class="{ active: currentStep >= 2 }">2</div>
                <div class="step-line"></div>
                <div class="step" :class="{ active: currentStep >= 3 }">3</div>
              </div>
              
              <div class="form-row">
                <div class="form-group" :class="{ focused: focusedField === 'name' }">
                  <label class="form-label">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                      <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2"/>
                      <circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>
                    </svg>
                    Ваше имя *
                  </label>
                  <input 
                    v-model="form.name"
                    type="text" 
                    placeholder="Введите ваше имя" 
                    required
                    class="form-input"
                    @focus="focusedField = 'name'"
                    @blur="focusedField = ''"
                  />
                  <div class="input-decoration"></div>
                </div>
                <div class="form-group" :class="{ focused: focusedField === 'phone' }">
                  <label class="form-label">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                      <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z" stroke="currentColor" stroke-width="2" fill="none"/>
                    </svg>
                    Телефон *
                  </label>
                  <input 
                    v-model="form.phone"
                    type="tel" 
                    placeholder="+7 (999) 999-99-99" 
                    required
                    class="form-input"
                    @focus="focusedField = 'phone'"
                    @blur="focusedField = ''"
                  />
                  <div class="input-decoration"></div>
                </div>
              </div>
              
              <div class="form-row">
                <div class="form-group" :class="{ focused: focusedField === 'email' }">
                  <label class="form-label">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                      <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z" stroke="currentColor" stroke-width="2" fill="none"/>
                      <polyline points="22,6 12,13 2,6" stroke="currentColor" stroke-width="2" fill="none"/>
                    </svg>
                    Email *
                  </label>
                  <input 
                    v-model="form.email"
                    type="email" 
                    placeholder="your.email@example.com" 
                    required
                    class="form-input"
                    @focus="focusedField = 'email'"
                    @blur="focusedField = ''"
                  />
                  <div class="input-decoration"></div>
                </div>
                <div class="form-group" :class="{ focused: focusedField === 'organization' }">
                  <label class="form-label">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                      <path d="M6 22V4a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v18Z" stroke="currentColor" stroke-width="2" fill="none"/>
                      <path d="M6 12h4m0 0h4m-4 0v4m-4-8h8" stroke="currentColor" stroke-width="2"/>
                    </svg>
                    Организация
                  </label>
                  <input 
                    v-model="form.organization"
                    type="text" 
                    placeholder="Название организации" 
                    class="form-input"
                    @focus="focusedField = 'organization'"
                    @blur="focusedField = ''"
                  />
                  <div class="input-decoration"></div>
                </div>
              </div>
              
              <div class="form-group" :class="{ focused: focusedField === 'message' }">
                <label class="form-label">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2v10z" stroke="currentColor" stroke-width="2" fill="none"/>
                  </svg>
                  Сообщение
                </label>
                <textarea 
                  v-model="form.message"
                  placeholder="Опишите что вас интересует" 
                  rows="4"
                  class="form-textarea"
                  @focus="focusedField = 'message'"
                  @blur="focusedField = ''"
                ></textarea>
                <div class="input-decoration"></div>
              </div>
              
              <div class="form-checkbox">
                <label class="checkbox-label" :class="{ checked: form.agreement }">
                  <input 
                    v-model="form.agreement"
                    type="checkbox" 
                    required
                  />
                  <div class="custom-checkbox">
                    <svg width="14" height="14" viewBox="0 0 24 24" fill="none">
                      <path d="M20 6L9 17l-5-5" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                  </div>
                  Я согласен на обработку персональных данных
                </label>
              </div>
              
              <button type="submit" class="submit-button" :disabled="!form.agreement || isSubmitting">
                <span class="button-content">
                  <span v-if="!isSubmitting">Отправить заявку</span>
                  <span v-else>Отправляем...</span>
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" v-if="!isSubmitting">
                    <path d="M5 12h14M12 5l7 7-7 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                  <div class="loading-spinner" v-else>
                    <div class="spinner"></div>
                  </div>
                </span>
                <div class="button-glow"></div>
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { ref, reactive, onMounted, onUnmounted } from 'vue'

export default {
  name: 'ContactForm',
  setup() {
    const sectionRef = ref(null)
    const isVisible = ref(false)
    const isSubmitting = ref(false)
    const focusedField = ref('')
    const currentStep = ref(1)
    
    const form = reactive({
      name: '',
      phone: '',
      email: '',
      organization: '',
      message: '',
      agreement: false
    })
    
    const submitForm = async () => {
      if (!form.agreement || isSubmitting.value) return
      
      isSubmitting.value = true
      currentStep.value = 3
      
      try {
        // Симуляция отправки
        await new Promise(resolve => setTimeout(resolve, 2000))
        
        console.log('Form submitted:', form)
        alert('Спасибо! Ваша заявка отправлена. Мы свяжемся с вами в ближайшее время!')
        
        // Очистка формы
        Object.keys(form).forEach(key => {
          if (key === 'agreement') {
            form[key] = false
          } else {
            form[key] = ''
          }
        })
        
        currentStep.value = 1
      } catch (error) {
        console.error('Error submitting form:', error)
        alert('Произошла ошибка. Попробуйте ещё раз.')
      } finally {
        isSubmitting.value = false
      }
    }
    
    const observeSection = () => {
      const observer = new IntersectionObserver(
        ([entry]) => {
          isVisible.value = entry.isIntersecting
          if (entry.isIntersecting) {
            currentStep.value = 2
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
      
      onUnmounted(() => {
        observer.disconnect()
      })
    })
    
    return {
      sectionRef,
      isVisible,
      isSubmitting,
      focusedField,
      currentStep,
      form,
      submitForm
    }
  }
}
</script>

<style scoped>
.contact-form {
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  position: relative;
  background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #334155 100%);
  padding: var(--spacing-3xl) 0;
  overflow: hidden;
}

.contact-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.animated-grid {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0.1;
}

.grid-line {
  position: absolute;
  width: 1px;
  height: 100%;
  background: linear-gradient(0deg, transparent, var(--color-primary), transparent);
  animation: gridMove 12s infinite ease-in-out;
}

@keyframes gridMove {
  0%, 100% { transform: translateY(-100%); opacity: 0; }
  50% { transform: translateY(0); opacity: 1; }
}

.floating-envelopes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.envelope {
  position: absolute;
  color: rgba(216, 4, 42, 0.2);
  animation: envelopeFloat 20s infinite linear;
}

@keyframes envelopeFloat {
  0% { transform: translateY(0) rotate(0deg); opacity: 0; }
  10% { opacity: 1; }
  50% { transform: translateY(-40vh) rotate(180deg); opacity: 0.6; }
  90% { opacity: 1; }
  100% { transform: translateY(-80vh) rotate(360deg); opacity: 0; }
}

.contact-glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(216, 4, 42, 0.08) 0%, rgba(255, 215, 0, 0.04) 30%, transparent 60%);
  animation: contactGlow 15s ease-in-out infinite alternate;
}

@keyframes contactGlow {
  0% { transform: scale(1) rotate(0deg); }
  100% { transform: scale(1.1) rotate(15deg); }
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
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
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

.form-container {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: var(--spacing-3xl);
  align-items: start;
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.form-container.visible {
  opacity: 1;
  transform: translateY(0);
}

.form-visual {
  position: relative;
}

.visual-container {
  position: relative;
}

.image-frame {
  position: relative;
  margin-bottom: var(--spacing-xl);
}

.frame-decoration {
  position: absolute;
  top: -15px;
  left: -15px;
  right: -15px;
  bottom: -15px;
  background: linear-gradient(135deg, rgba(255, 215, 0, 0.3), rgba(216, 4, 42, 0.3));
  border-radius: 35px;
  filter: blur(20px);
  opacity: 0.6;
  animation: frameDecoration 4s ease-in-out infinite alternate;
}

@keyframes frameDecoration {
  0% { transform: scale(1); }
  100% { transform: scale(1.03); }
}

.image-wrapper {
  position: relative;
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 0 25px 70px rgba(0, 0, 0, 0.4);
}

.image-wrapper img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  display: block;
  transition: transform 0.5s ease;
}

.form-visual:hover .image-wrapper img {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(15, 23, 42, 0.8) 0%, rgba(30, 41, 59, 0.6) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.form-visual:hover .image-overlay {
  opacity: 1;
}

.overlay-content {
  text-align: center;
  color: white;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.form-visual:hover .overlay-content {
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
  color: #0f172a;
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

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.info-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  padding: 20px;
  display: flex;
  align-items: center;
  gap: 15px;
  transition: all 0.3s ease;
  animation: infoCardFloat 4s ease-in-out infinite alternate;
}

.info-card:nth-child(2) {
  animation-delay: 1s;
}

.info-card:nth-child(3) {
  animation-delay: 2s;
}

@keyframes infoCardFloat {
  0% { transform: translateY(0); }
  100% { transform: translateY(-8px); }
}

.info-card:hover {
  transform: translateY(-5px) scale(1.02);
  box-shadow: 0 15px 40px rgba(255, 215, 0, 0.15);
}

.info-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #0f172a;
  flex-shrink: 0;
}

.info-text {
  display: flex;
  flex-direction: column;
}

.info-label {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 2px;
}

.info-value {
  font-size: 1.1rem;
  font-weight: var(--font-weight-semibold);
  color: white;
}

.form-content {
  position: relative;
}

.form-wrapper {
  position: relative;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 30px;
  padding: var(--spacing-3xl);
  overflow: hidden;
}

.form-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  opacity: 0.03;
}

.form-pattern {
  width: 100%;
  height: 100%;
  background-image: radial-gradient(circle at 25px 25px, rgba(255, 255, 255, 0.4) 2px, transparent 2px);
  background-size: 50px 50px;
  animation: formPatternMove 20s linear infinite;
}

@keyframes formPatternMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

.contact-form-wrapper {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.form-steps {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: var(--spacing-xl);
}

.step {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  border: 2px solid rgba(255, 255, 255, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255, 255, 255, 0.6);
  font-weight: var(--font-weight-bold);
  transition: all 0.5s ease;
}

.step.active {
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-color: #ffd700;
  color: #0f172a;
  transform: scale(1.1);
}

.step-line {
  width: 50px;
  height: 2px;
  background: rgba(255, 255, 255, 0.2);
  margin: 0 10px;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--spacing-lg);
}

.form-group {
  position: relative;
  transition: all 0.3s ease;
}

.form-group.focused {
  transform: translateY(-5px);
}

.form-label {
  display: flex;
  align-items: center;
  gap: 10px;
  color: rgba(255, 255, 255, 0.9);
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
  margin-bottom: 8px;
}

.form-label svg {
  color: #ffd700;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 18px 20px;
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 15px;
  color: white;
  font-size: 1rem;
  font-family: var(--font-primary);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  backdrop-filter: blur(10px);
}

.form-input::placeholder,
.form-textarea::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: #ffd700;
  background: rgba(255, 255, 255, 0.1);
  box-shadow: 0 0 0 4px rgba(255, 215, 0, 0.1);
  transform: translateY(-2px);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
}

.input-decoration {
  position: absolute;
  bottom: -2px;
  left: 20px;
  right: 20px;
  height: 2px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 1px;
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.form-group.focused .input-decoration {
  transform: scaleX(1);
}

.form-checkbox {
  display: flex;
  align-items: flex-start;
  gap: 15px;
  margin: var(--spacing-lg) 0;
}

.checkbox-label {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.9);
  font-size: 0.95rem;
  line-height: 1.5;
  transition: all 0.3s ease;
}

.checkbox-label:hover {
  color: white;
}

.checkbox-label input {
  opacity: 0;
  position: absolute;
  pointer-events: none;
}

.custom-checkbox {
  width: 24px;
  height: 24px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  flex-shrink: 0;
  margin-top: 2px;
}

.checkbox-label.checked .custom-checkbox {
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-color: #ffd700;
}

.custom-checkbox svg {
  opacity: 0;
  transform: scale(0);
  transition: all 0.2s ease;
  color: #0f172a;
}

.checkbox-label.checked .custom-checkbox svg {
  opacity: 1;
  transform: scale(1);
}

.submit-button {
  position: relative;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  color: #0f172a;
  border: none;
  padding: 20px 40px;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: var(--font-weight-bold);
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 15px 40px rgba(255, 215, 0, 0.3);
  align-self: center;
  min-width: 250px;
  overflow: hidden;
}

.submit-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transition: left 0.6s ease;
}

.submit-button:not(:disabled):hover::before {
  left: 100%;
}

.submit-button:not(:disabled):hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 20px 50px rgba(255, 215, 0, 0.4);
}

.submit-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  transform: none;
}

.button-content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  position: relative;
  z-index: 2;
}

.loading-spinner {
  width: 20px;
  height: 20px;
}

.spinner {
  width: 100%;
  height: 100%;
  border: 2px solid rgba(15, 23, 42, 0.3);
  border-top: 2px solid #0f172a;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.button-glow {
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(135deg, #ffd700, #ff8c00);
  border-radius: 52px;
  opacity: 0;
  filter: blur(10px);
  transition: opacity 0.3s ease;
  z-index: -1;
}

.submit-button:not(:disabled):hover .button-glow {
  opacity: 0.5;
}

@media (max-width: 1200px) {
  .form-container {
    grid-template-columns: 1fr;
    gap: var(--spacing-2xl);
  }
  
  .contact-info {
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: var(--spacing-lg);
  }
}

@media (max-width: 768px) {
  .contact-form {
    padding: var(--spacing-2xl) 0;
  }
  
  .form-wrapper {
    padding: var(--spacing-2xl);
  }
  
  .form-row {
    grid-template-columns: 1fr;
    gap: var(--spacing-md);
  }
  
  .image-wrapper img {
    height: 300px;
  }
  
  .contact-info {
    flex-direction: column;
    align-items: center;
  }
  
  .info-card {
    width: 100%;
    max-width: 280px;
  }
  
  .submit-button {
    min-width: auto;
    width: 100%;
  }
}
</style>