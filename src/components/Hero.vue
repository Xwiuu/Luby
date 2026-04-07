<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const titleRef = ref(null)
const imageRef = ref(null)
const ctaRef = ref(null)

onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: 'power4.out', duration: 1.5 } });

  tl.from(imageRef.value, { 
    x: 100, 
    opacity: 0, 
    scale: 1.1,
    filter: 'blur(10px)' 
  })
  .from(titleRef.value, { 
    y: 60, 
    opacity: 0,
    stagger: 0.2 
  }, "-=1.2")
  .from(ctaRef.value, { 
    y: 20, 
    opacity: 0 
  }, "-=1");
})
</script>

<template>
  <section class="relative min-h-[80vh] lg:min-h-screen flex items-center bg-[#FFF5F2] overflow-hidden pt-20 pb-16 sm:pb-20">
    <div class="absolute top-0 right-0 w-1/2 h-full bg-linear-to-l from-[#F4C2C2]/20 to-transparent"></div>

    <div class="container mx-auto px-6 sm:px-8 lg:px-12 grid grid-cols-1 lg:grid-cols-12 gap-12 items-center relative z-10">
      
      <div class="col-span-1 lg:col-span-6 text-center lg:text-left">
        <div class="inline-flex items-center gap-2 mb-8 bg-white/50 backdrop-blur-sm px-4 py-2 rounded-full border border-luby-gold/20">
          <span class="w-2 h-2 rounded-full bg-luby-gold animate-pulse"></span>
          <span class="text-[10px] font-mono tracking-[0.3em] uppercase text-gray-600">Seja uma consultora Luby</span>
        </div>

        <h1 ref="titleRef" class="font-brielle text-4xl sm:text-5xl md:text-6xl lg:text-7xl leading-[0.92] mb-8 text-gray-950">
          Sua nova jornada <br>
          <span class="text-luby-gold italic font-light">começa com brilho.</span>
        </h1>

        <p class="text-gray-600 text-base sm:text-lg md:text-xl max-w-xl mx-auto lg:mx-0 mb-10 leading-relaxed">
          Transforme sua paixão por <span class="text-gray-900 font-medium">semijoias</span> em um negócio lucrativo e sofisticado. Risco zero, suporte total e elegância em cada peça.
        </p>

      </div>

      <div class="col-span-1 lg:col-span-6 mt-10 lg:mt-0 relative flex justify-center lg:justify-end">
        <div ref="imageRef" class="relative w-full max-w-xl sm:max-w-2xl lg:max-w-xl aspect-3/4 rounded-[4rem] overflow-hidden shadow-[-40px_40px_80px_rgba(244,194,194,0.4)] border-8 border-white">
          <img 
            src="../assets/hero.jpeg" 
            alt="Revendedora Luby" 
            class="w-full h-full object-cover"
          >
          
          <div class="absolute inset-0 bg-linear-to-t from-[#F4C2C2]/20 to-transparent mix-blend-multiply"></div>
        </div>

        <div class="absolute -bottom-6 left-1/2 -translate-x-1/2 md:-left-12 bg-white p-5 sm:p-6 rounded-3xl shadow-xl flex items-center gap-4 animate-bounce-slow max-w-[calc(100%-2rem)] md:max-w-none">
          <div class="w-12 h-12 bg-luby-gold rounded-full flex items-center justify-center text-white font-bold italic">L</div>
          <div>
            <p class="text-[10px] font-mono uppercase text-gray-400">Qualidade</p>
            <p class="font-brielle text-lg">Semijoias Premium</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.animate-bounce-slow {
  animation: bounce 4s infinite ease-in-out;
}
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}
</style>