<template>
  <header class="header" :class="{ 'scrolled': isScrolled }">
    <div class="container">
      <nav class="nav">
        <div class="logo">
          <img src="/assets/images/logo.png" alt="EXPO REAL ESTATE" />
        </div>
        
        <div class="nav-links" :class="{ 'active': mobileMenuOpen }">
          <a href="#about" @click="closeMenu">О&nbsp;выставке</a>
          <a href="#benefits" @click="closeMenu">Преимущества</a>
          <a href="#participants" @click="closeMenu">Участники</a>
          <a href="#contacts" @click="closeMenu">Контакты</a>
        </div>
        
        <div class="header-contacts">
          <a href="mailto:org@exporealestate.ru" class="contact-link">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
              <path d="M18 4H2C1.45 4 1 4.45 1 5V15C1 15.55 1.45 16 2 16H18C18.55 16 19 15.55 19 15V5C19 4.45 18.55 4 18 4ZM17.5 6L10 10.5L2.5 6H17.5ZM2.5 14V7.5L10 12L17.5 7.5V14H2.5Z" fill="currentColor"/>
            </svg>
            org@exporealestate.ru
          </a>
          <a href="tel:+74993500006" class="contact-link">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
              <path d="M15.54 12.92L13.5 11.69C13.02 11.39 12.39 11.49 12.02 11.93L11.5 12.56C11.43 12.65 11.31 12.68 11.2 12.64C10.63 12.43 9.38 11.55 8.57 10.74C7.76 9.93 6.88 8.68 6.67 8.11C6.63 8 6.66 7.88 6.75 7.81L7.38 7.29C7.82 6.92 7.92 6.29 7.62 5.81L6.39 3.77C6.06 3.24 5.36 3.11 4.87 3.48L3.91 4.21C3.5 4.52 3.24 4.99 3.2 5.5C3.08 7.13 3.66 9.25 5.97 11.56C8.28 13.87 10.4 14.45 12.03 14.33C12.54 14.29 13.01 14.03 13.32 13.62L14.05 12.66C14.42 12.17 14.29 11.47 13.76 11.14L15.54 12.92Z" fill="currentColor"/>
            </svg>
            +7 (499) 35 0000 6
          </a>
        </div>
        
        <button class="btn btn-header" @click="openModal">
          Получить билет
        </button>
        
        <button class="mobile-toggle" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </nav>
    </div>
  </header>
</template>

<script>
import { ref, onMounted, onUnmounted, inject } from 'vue'

export default {
  name: 'Header',
  setup() {
    const isScrolled = ref(false)
    const mobileMenuOpen = ref(false)
    const openModal = inject('openModal')
    
    const handleScroll = () => {
      isScrolled.value = window.scrollY > 50
    }
    
    const toggleMobileMenu = () => {
      mobileMenuOpen.value = !mobileMenuOpen.value
    }
    
    const closeMenu = () => {
      mobileMenuOpen.value = false
    }
    
    onMounted(() => {
      window.addEventListener('scroll', handleScroll)
    })
    
    onUnmounted(() => {
      window.removeEventListener('scroll', handleScroll)
    })
    
    return {
      isScrolled,
      mobileMenuOpen,
      toggleMobileMenu,
      closeMenu,
      openModal
    }
  }
}
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  transition: var(--transition);
}

.header.scrolled {
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
}

.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 0;
  gap: 2rem;
}

.logo img {
  height: 50px;
  width: auto;
}

.nav-links {
  display: flex;
  gap: clamp(1rem, 3vw, 2.5rem);
  flex: 1;
  justify-content: center;
  align-items: center;
}

.nav-links a {
  font-weight: var(--font-weight-medium);
  color: var(--color-text);
  position: relative;
  padding: 0.5rem 0.25rem;
  font-size: clamp(0.85rem, 2.5vw, 1rem);
  white-space: nowrap;
  text-align: center;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background-color: var(--color-primary);
  transition: width 0.3s;
}

.nav-links a:hover::after {
  width: 100%;
}

.header-contacts {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  color: var(--color-text);
  font-size: clamp(0.7rem, 2vw, 0.85rem);
  white-space: nowrap;
}

.contact-link:hover {
  color: var(--color-primary);
}

.contact-link svg {
  flex-shrink: 0;
}

.btn-header {
  padding: 0.75rem 2rem;
  font-size: 0.95rem;
}

.mobile-toggle {
  display: none;
  flex-direction: column;
  gap: 4px;
  background: transparent;
  padding: 0.5rem;
}

.mobile-toggle span {
  width: 25px;
  height: 2px;
  background-color: var(--color-text);
  transition: var(--transition);
}

@media (max-width: 1200px) {
  .nav-links {
    gap: clamp(0.5rem, 2vw, 1.5rem);
  }
  
  .nav-links a {
    font-size: clamp(0.8rem, 2.2vw, 0.95rem);
    padding: 0.5rem 0.15rem;
  }
}

@media (max-width: 1024px) {
  .header-contacts .contact-link:last-child {
    display: none;
  }
  
  .btn-header {
    padding: 0.6rem 1.5rem;
    font-size: 0.85rem;
  }
}

@media (max-width: 900px) {
  .header-contacts {
    display: none;
  }
  
  .nav-links {
    gap: clamp(0.8rem, 3vw, 1.5rem);
  }
}

@media (max-width: 768px) {
  .nav {
    padding: 0.75rem 0;
  }
  
  .logo img {
    height: 45px;
  }
  
  .nav-links {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    background: rgba(255, 255, 255, 0.98);
    backdrop-filter: blur(20px);
    flex-direction: column;
    padding: 2rem;
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
    gap: 1.5rem;
    z-index: 999;
  }
  
  .nav-links a {
    font-size: 1.1rem;
    padding: 1rem 0;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
  }
  
  .nav-links.active {
    transform: translateX(0);
  }
  
  .mobile-toggle {
    display: flex;
  }
  
  .btn-header {
    padding: 0.6rem 1.2rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .nav {
    padding: 0.5rem 0;
  }
  
  .logo img {
    height: 40px;
  }
  
  .btn-header {
    padding: 0.5rem 1rem;
    font-size: 0.75rem;
    border-radius: 20px;
  }
}
</style>