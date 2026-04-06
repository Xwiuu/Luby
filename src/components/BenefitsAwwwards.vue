<script setup lang="ts">
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Animação de entrada dos cards: 
  // IMPORTANTE: Adicionado 'clearProps' para evitar que o GSAP trave o estilo após animar
  gsap.from(".benefit-card", {
    y: 30,
    opacity: 0,
    duration: 0.8,
    stagger: 0.1,
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".benefits-grid",
      start: "top 85%",
      toggleActions: "play none none none"
    },
    onComplete: () => {
       gsap.set(".benefit-card", { clearProps: "all" })
    }
  })

  // Flutuação contínua dos ícones (Sutil)
  gsap.to(".icon-float", {
    y: -5,
    duration: 2,
    yoyo: true,
    repeat: -1,
    ease: "sine.inOut",
    stagger: 0.2
  })
})
</script>

<template>
  <section 
    ref="sectionRef" 
    class="relative z-20 bg-[#FFF9F7] pt-16 sm:pt-20 md:pt-24 pb-16 sm:pb-24 md:pb-32 rounded-t-[3rem] overflow-hidden shadow-sm"
  >
    <div class="absolute top-0 right-0 w-[200px] h-[200px] sm:w-[250px] sm:h-[250px] md:w-[300px] md:h-[300px] bg-[#F4C2C2] opacity-20 blur-[100px] rounded-full pointer-events-none"></div>
    <div class="absolute bottom-0 left-0 w-[200px] h-[200px] sm:w-[250px] sm:h-[250px] md:w-[300px] md:h-[300px] bg-luby-gold opacity-10 blur-[100px] rounded-full pointer-events-none"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 relative z-10">
      
      <div class="text-center max-w-2xl mx-auto mb-12 sm:mb-14 md:mb-16">
        <div class="inline-flex items-center gap-2 mb-3 sm:mb-4 bg-white px-3 sm:px-4 py-1 sm:py-1.5 rounded-full border border-[#F4C2C2]/20">
          <span class="w-1.5 h-1.5 rounded-full bg-luby-gold"></span>
          <span class="text-[9px] sm:text-[10px] font-mono tracking-[0.3em] uppercase text-gray-500">Diferenciais Luby</span>
        </div>
        <h2 class="text-3xl sm:text-4xl md:text-6xl font-brielle text-gray-900 leading-tight">
          Feito para você <br>
          <span class="text-luby-gold italic font-light">brilhar conosco.</span>
        </h2>
      </div>

      <div class="benefits-grid grid grid-cols-1 md:grid-cols-12 gap-4 sm:gap-6">
        
        <div class="benefit-card md:col-span-8 group relative rounded-[2rem] sm:rounded-[2.5rem] bg-white border border-gray-100 p-6 sm:p-8 md:p-12 flex flex-col justify-between min-h-[280px] sm:min-h-[300px] transition-all duration-500 hover:shadow-xl hover:border-luby-gold/20">
          <div class="flex justify-between items-start">
            <div class="icon-float w-12 h-12 sm:w-14 md:w-16 h-12 sm:h-14 md:h-16 rounded-2xl bg-[#FFF5F2] flex items-center justify-center text-luby-gold border border-white shadow-sm">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 3h12l4 6-10 13L2 9Z"/><path d="M11 3 8 9l4 13 4-13-3-6"/><path d="M2 9h20"/></svg>
            </div>
            <span class="text-[9px] sm:text-[10px] font-mono text-gray-300 uppercase tracking-widest">01 / Ganhos</span>
          </div>
          <div>
            <h3 class="text-xl sm:text-2xl md:text-3xl font-brielle text-gray-900 mb-2 sm:mb-3">Margem de Lucro Real</h3>
            <p class="text-gray-500 text-sm sm:text-base md:text-lg max-w-md">
              Semijoias com alto valor percebido que garantem ganhos extraordinários por peça vendida.
            </p>
          </div>
        </div>

        <div class="benefit-card md:col-span-4 group relative rounded-[2rem] sm:rounded-[2.5rem] bg-[#F4C2C2] p-6 sm:p-8 md:p-10 flex flex-col justify-between min-h-[280px] sm:min-h-[300px] shadow-lg shadow-[#F4C2C2]/20">
          <div class="icon-float w-10 h-10 sm:w-12 md:w-14 h-10 sm:h-12 md:h-14 rounded-full bg-white/30 flex items-center justify-center text-white backdrop-blur-md">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="14" x="2" y="5" rx="2"/><line x1="2" x2="22" y1="10" y2="10"/></svg>
          </div>
          <div class="text-white">
            <h3 class="text-xl sm:text-2xl font-brielle mb-2">Consignado sem risco</h3>
            <p class="text-white/90 text-xs sm:text-sm leading-relaxed">
              Nós investimos no seu estoque inicial. Você só paga o que vender.
            </p>
          </div>
        </div>

        <div class="benefit-card md:col-span-5 group relative rounded-[2rem] sm:rounded-[2.5rem] bg-[#1A1A1A] p-6 sm:p-8 md:p-10 flex flex-col justify-between min-h-[280px] sm:min-h-[300px]">
           <div class="icon-float w-10 h-10 sm:w-12 md:w-14 h-10 sm:h-12 md:h-14 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-luby-gold">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
          </div>
          <div class="text-white">
            <h3 class="text-xl sm:text-2xl font-brielle mb-2 text-luby-gold">Suporte Elite</h3>
            <p class="text-gray-400 text-xs sm:text-sm leading-relaxed">
              Fotos profissionais e material de marketing prontos para você usar.
            </p>
          </div>
        </div>

        <div class="benefit-card md:col-span-7 group relative rounded-[2rem] sm:rounded-[2.5rem] bg-white border border-gray-100 p-6 sm:p-8 md:p-10 flex items-center min-h-[280px] sm:min-h-[300px] hover:shadow-xl transition-all duration-500">
          <div class="flex flex-col md:flex-row gap-4 sm:gap-6 items-center md:items-start text-center md:text-left">
            <div class="icon-float shrink-0 w-12 h-12 sm:w-14 md:w-16 h-12 sm:h-14 md:h-16 rounded-full bg-[#FFF5F2] flex items-center justify-center text-luby-gold border border-[#F4C2C2]/20">
               <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/></svg>
            </div>
            <div>
              <h3 class="text-xl sm:text-2xl md:text-3xl font-brielle text-gray-900 mb-2">Design que Encanta</h3>
              <p class="text-gray-500 text-xs sm:text-sm md:text-base leading-relaxed">
                Curadoria de semijoias selecionadas para garantir o desejo imediato das suas clientes.
              </p>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
/* Garante que as fontes carreguem e o espaçamento seja respeitado */
.font-brielle {
  letter-spacing: -0.01em;
}
.benefit-card {
  will-change: transform, opacity;
}
</style>