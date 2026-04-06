<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { gsap } from 'gsap'

// Refs para os elementos
const sectionRef = ref<HTMLElement | null>(null);
const titleRef = ref<HTMLElement | null>(null);
const mainVisual = ref<HTMLElement | null>(null);
const subtext = ref<HTMLElement | null>(null);
const cta = ref<HTMLElement | null>(null);
const productItems = ref<Element[]>([]);

// Helper para múltiplos refs
const addToRefs = (el: any) => {
  if (el instanceof Element && !productItems.value.includes(el)) {
    productItems.value.push(el);
  }
};

onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: 'power3.out', duration: 1.2 } });

  // 1. ANIMAÇÃO DE ENTRADA (HMR)
  // Animação mais suave e lenta, condizente com o novo visual
  tl.from(titleRef.value, { y: 40, opacity: 0, delay: 0.2 })
    .from(subtext.value, { y: 20, opacity: 0, duration: 1 }, "-=0.8")
    .from(cta.value, { y: 20, opacity: 0, duration: 1 }, "-=0.8")
    .from(mainVisual.value, { scale: 1.05, opacity: 0, duration: 2 }, 0.5);

  // 2. EFEITO PARALLAX NO MOUSE (Suavizado)
  const mouseMoveHandler = (e: MouseEvent) => {
    if (!sectionRef.value || window.innerWidth < 1024) return;
    
    const { clientX, clientY } = e;
    const centerX = window.innerWidth / 2;
    const centerY = window.innerHeight / 2;
    const deltaX = clientX - centerX;
    const deltaY = clientY - centerY;

    productItems.value.forEach((item, index) => {
      // Fator de movimento reduzido para ser mais sutil
      const factor = (index + 1) * 30; 
      gsap.to(item, {
        x: deltaX / factor,
        y: deltaY / factor,
        duration: 0.8,
        ease: 'power1.out',
      });
    });
  };

  window.addEventListener('mousemove', mouseMoveHandler);

  onUnmounted(() => {
    window.removeEventListener('mousemove', mouseMoveHandler);
  });
});
</script>

<template>
  <section ref="sectionRef" class="relative min-h-screen flex items-center justify-center pt-20 sm:pt-24 md:pt-32 lg:pt-24 overflow-hidden bg-[#FFF5F2] text-[#1A1A1A]">
    
    <div class="absolute inset-0 z-0 opacity-40">
      <div class="absolute -top-10 -right-10 sm:-top-20 sm:-right-20 lg:-top-40 lg:-right-40 w-32 h-32 sm:w-64 sm:h-64 lg:w-96 lg:h-96 rounded-full bg-luby-gold/20 blur-3xl"></div>
      <div class="absolute bottom-10 -left-5 sm:bottom-20 sm:-left-10 lg:-left-20 w-32 h-32 sm:w-64 sm:h-64 lg:w-80 lg:h-80 rounded-full bg-[#F4C2C2]/40 blur-2xl"></div>
    </div>

    <div class="container relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-12 grid grid-cols-12 gap-6 sm:gap-8 lg:gap-12 items-center">
      
      <div class="col-span-12 lg:col-span-6 flex flex-col justify-center text-center lg:text-left">
        <div class="inline-flex items-center gap-2 sm:gap-3 mb-4 sm:mb-6 self-center lg:self-start opacity-80">
          <span class="w-1.5 h-1.5 rounded-full bg-luby-gold animate-pulse"></span>
          <span class="text-[10px] sm:text-xs font-mono tracking-widest uppercase text-luby-gold">Oportunidade Exclusiva</span>
        </div>

        <h1 ref="titleRef" class="font-brielle text-3xl sm:text-4xl md:text-5xl lg:text-7xl xl:text-[5.5rem] leading-[1.1] md:leading-none mb-6 sm:mb-8 md:mb-10 -ml-1 flex flex-col items-center lg:items-start tracking-tight">
          Sua jornada de <br>
          <span class="text-luby-gold italic font-light">brilho e conquista.</span>
        </h1>

        <p ref="subtext" class="text-base sm:text-lg md:text-2xl font-sans text-gray-700 leading-relaxed mb-8 sm:mb-10 md:mb-12 max-w-xl mx-auto lg:mx-0 px-2 sm:px-0">
          Transforme sofisticação em <strong class="text-luby-gold font-medium">renda extraordinária</strong>. Torne-se uma revendedora exclusiva Luby Semijoias e conquiste sua liberdade com estilo.
        </p>

        <div ref="cta" class="lg:self-start self-center">
           <button class="bg-[#1A1A1A] text-white px-6 sm:px-8 md:px-12 py-3 sm:py-4 md:py-5 rounded-full font-semibold text-sm sm:text-base uppercase tracking-widest hover:bg-luby-gold transition-all duration-300 shadow-xl transform hover:-translate-y-1">
             Conversar com consultora
           </button>
        </div>
      </div>

      <div ref="mainVisual" class="col-span-12 lg:col-span-6 relative flex items-center justify-center mt-12 sm:mt-16 md:mt-20 lg:mt-0">
        <div class="relative w-full max-w-[280px] sm:max-w-[320px] md:max-w-xl aspect-[4/5] rounded-[1.5rem] sm:rounded-[2rem] overflow-hidden shadow-2xl border-2 sm:border-4 border-white">
          <img src="https://images.unsplash.com/photo-1549463428-f6825c9381e4?q=80&w=1000&auto=format&fit=crop" alt="Mulher usando Semijoias Luby" class="w-full h-full object-cover">
        </div>

        <div :ref="addToRefs" class="absolute -right-4 -top-6 sm:-right-8 sm:-top-12 md:-right-16 md:-top-16 w-20 h-20 sm:w-32 sm:h-32 md:w-44 md:h-44 rounded-full border border-gray-100 bg-white p-2 sm:p-3 shadow-2xl hidden sm:flex items-center justify-center text-[8px] sm:text-[10px] text-gray-400">
          [Colar Rosé]
        </div>

        <div :ref="addToRefs" class="absolute -left-6 bottom-6 sm:-left-12 sm:bottom-12 md:-left-20 md:bottom-20 w-18 h-18 sm:w-28 sm:h-28 md:w-36 md:h-36 rounded-full border border-gray-100 bg-white p-2 sm:p-3 shadow-2xl hidden sm:flex items-center justify-center text-[8px] sm:text-[10px] text-gray-400">
          [Brinco Ouro]
        </div>
      </div>
    </div>

    <div class="absolute bottom-4 sm:bottom-6 md:bottom-8 left-1/2 transform -translate-x-1/2 hidden md:flex flex-col items-center gap-1 sm:gap-2 opacity-50">
      <span class="text-[10px] sm:text-xs font-mono uppercase tracking-widest text-gray-600">Scroll</span>
      <div class="w-[1px] h-12 sm:h-16 bg-gray-300 relative overflow-hidden">
        <div class="absolute top-0 left-0 w-full h-full bg-luby-gold animate-scroll-line"></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.font-brielle {
  letter-spacing: -0.01em;
}

@keyframes scroll-line {
  0% { transform: translateY(-100%); }
  100% { transform: translateY(100%); }
}
.animate-scroll-line {
  animation: scroll-line 1.5s infinite;
}
</style>