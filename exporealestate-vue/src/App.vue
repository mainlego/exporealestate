<template>
  <div id="app">
    <Header />
    <HeroSection />
    <StatsSection />
    <BenefitsSection />
    <WhyVisitSection />
    <ParticipantsSection />
    <GeographySection />
    <AdvantagesSection />
    <InvestmentTypes />
    <ShowroomSection />
    <ContactForm />
    <PartnersSection />
    <Footer />
    <ModalForm v-if="showModal" @close="showModal = false" />
  </div>
</template>

<script>
import { ref, provide } from 'vue'
import Header from './components/Header.vue'
import HeroSection from './components/HeroSection.vue'
import StatsSection from './components/StatsSection.vue'
import BenefitsSection from './components/BenefitsSection.vue'
import WhyVisitSection from './components/WhyVisitSection.vue'
import ParticipantsSection from './components/ParticipantsSection.vue'
import GeographySection from './components/GeographySection.vue'
import AdvantagesSection from './components/AdvantagesSection.vue'
import InvestmentTypes from './components/InvestmentTypes.vue'
import ShowroomSection from './components/ShowroomSection.vue'
import ContactForm from './components/ContactForm.vue'
import PartnersSection from './components/PartnersSection.vue'
import Footer from './components/Footer.vue'
import ModalForm from './components/ModalForm.vue'

export default {
  name: 'App',
  components: {
    Header,
    HeroSection,
    StatsSection,
    BenefitsSection,
    WhyVisitSection,
    ParticipantsSection,
    GeographySection,
    AdvantagesSection,
    InvestmentTypes,
    ShowroomSection,
    ContactForm,
    PartnersSection,
    Footer,
    ModalForm
  },
  setup() {
    const showModal = ref(false)
    
    const openModal = () => {
      showModal.value = true
    }
    
    provide('openModal', openModal)
    
    return {
      showModal
    }
  }
}
</script>

<style>
@import './assets/main.css';

html, body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  width: 100%;
  max-width: 100vw;
}

#app {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  width: 100%;
  max-width: 100vw;
  overflow-x: hidden;
}
</style>
