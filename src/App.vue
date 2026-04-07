<script setup lang="ts">
import HeaderGlass from './components/HeaderGlass.vue'
import Hero from './components/Hero.vue'
import BenefitsAwwwards from './components/BenefitsAwwwards.vue'
import HowItWorks from './components/HowItWorks.vue'
import BusinessModel from './components/BusinessModel.vue'
import SocialProof from './components/SocialProof.vue'
import FinalCta from './components/FinalCta.vue'
import Faq from './components/Faq.vue'
import Footer from './components/Footer.vue'
import OurStory from './components/OurStory.vue'
</script>

<template>
  <div class="min-h-screen relative bg-luby-nude overflow-x-hidden">
    <HeaderGlass />
    
    <main>
      <Hero id="inicio" />

      <OurStory id="nossa-historia" />
      
      <BenefitsAwwwards id="beneficios" />
      
      <HowItWorks id="como-funciona" />
      
      <BusinessModel id="ganhos" /> 
      
      <SocialProof />

      <FinalCta />
      
      <Faq id="faq" />
    </main>

    <Footer />
  </div>
</template>

<style>
/* Reset básico para evitar scroll horizontal fantasma no Android */
html, body {
  max-width: 100vw;
  overflow-x: hidden;
  margin: 0;
  padding: 0;
}

/* Scroll suave nativo para navegadores que não suportam JS ou caso o GSAP demore a carregar */
html {
  scroll-behavior: smooth;
}
</style>