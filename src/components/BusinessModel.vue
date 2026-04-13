<script setup lang="ts">
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const commissions = [
  { label: "Semente", percent: 20, desc: "Seu primeiro passo com segurança.", range: "Até R$ 700" },
  { label: "Crescimento", percent: 30, desc: "Acelerando sua independência.", range: "R$ 701 a R$ 1.000" },
  { label: "Expansão", percent: 40, desc: "Construindo uma carreira sólida.", range: "R$ 1.001 a R$ 2.000" },
  { label: "Elite Luby", percent: 50, desc: "O topo do sucesso em semijoias.", range: "Acima de R$ 2.001" },
]

onMounted(() => {
  // Animação dos números (Contador e Revelação) - O layout que você curtiu
  const rows = gsap.utils.toArray('.comm-item')
  rows.forEach((row: any, i) => {
    const num = row.querySelector('.num-val')
    const target = commissions[i].percent

    gsap.from(row, {
      opacity: 0,
      x: i % 2 === 0 ? -50 : 50,
      duration: 1.2,
      ease: "power3.out",
      scrollTrigger: {
        trigger: row,
        start: "top 85%",
        toggleActions: "play none none reverse"
      }
    })

    // Contador dos números
    gsap.to(num, {
      innerText: target,
      duration: 2,
      snap: { innerText: 1 },
      ease: "power2.out",
      scrollTrigger: {
        trigger: row,
        start: "top 85%",
      }
    })
  })
})
</script>

<template>
  <section 
    ref="sectionRef" 
    class="relative bg-[#FFF5F2] text-[#1A1A1A] py-20 sm:py-24 md:py-32 overflow-hidden z-30 rounded-t-[4rem] -mt-16"
  >
    <div class="absolute top-0 left-0 w-full h-full pointer-events-none opacity-30">
      <div class="absolute top-1/4 -left-10 sm:-left-20 w-48 h-48 sm:w-96 sm:h-96 bg-luby-gold rounded-full blur-[150px]"></div>
    </div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 relative z-10">
      
      <div class="mb-16 sm:mb-20 md:mb-24">
        <div class="inline-flex items-center gap-3 sm:gap-4 mb-6 sm:mb-8">
          <div class="h-px w-12 sm:w-16 md:w-20 bg-luby-gold\"></div>
          <span class="text-luby-gold font-mono text-[10px] sm:text-xs tracking-[0.4em] uppercase">Plano de Ganhos</span>
        </div>
        <h2 class="text-3xl sm:text-4xl md:text-5xl lg:text-7xl font-brielle leading-[1.1] mb-8 sm:mb-10 md:mb-12">
          Comissões que <br> 
          <span class="italic text-gray-400 font-light">brilham com você.</span>
        </h2>
        <p class="max-w-xl text-gray-600 text-base sm:text-lg md:text-xl font-light leading-relaxed">
          Nós investimos no seu estoque para você focar no que importa. 
          <span class="text-[#1A1A1A] font-medium italic">Semijoias premium com risco zero e lucro extraordinário.</span>
        </p>
      </div>

      <div class="grid grid-cols-1">
        <div 
          v-for="(item, index) in commissions" 
          :key="index"
          class="comm-item group relative py-8 sm:py-10 md:py-12 border-b border-gray-200 flex flex-col md:flex-row md:items-center justify-between transition-all duration-500 hover:border-luby-gold"
        >
          <div class="max-w-sm mb-4 sm:mb-6 md:mb-0 transform group-hover:translate-x-4 transition-transform duration-500">
            <span class="text-luby-gold font-mono text-[10px] sm:text-xs uppercase tracking-widest mb-2 block">{{ item.label }}</span>
            <h4 class="text-xl sm:text-2xl font-brielle text-[#1A1A1A] mb-2">{{ item.range }}</h4>
            <p class="text-gray-500 text-xs sm:text-sm italic">{{ item.desc }}</p>
          </div>

          <div class="relative flex items-center justify-center md:justify-end">
             <div class="flex items-baseline font-brielle transition-all duration-500 group-hover:scale-105">
                <span class="num-val text-6xl sm:text-7xl md:text-8xl lg:text-[11rem] leading-none text-transparent bg-clip-text bg-linear-to-b from-gray-300 to-gray-500 group-hover:from-luby-gold group-hover:to-[#b8860b]">
                  0
                </span>
                <span class="text-3xl sm:text-4xl md:text-6xl text-luby-gold ml-1 sm:ml-2">%</span>
             </div>
          </div>
        </div>
      </div>

<div class="mt-16 sm:mt-20 md:mt-24 flex flex-col items-center">
        <a href="https://api.whatsapp.com/send/?phone=555484249459&text=Ol%C3%A1%21+Vi+a+p%C3%A1gina+de+vendas+da+Luby+e+estou+pronta+para+come%C3%A7ar+minha+nova+fase+de+brilho%21&type=phone_number&app_absent=0" target="_blank" class="relative bg-[#1A1A1A] text-white px-8 sm:px-10 md:px-12 py-4 sm:py-5 md:py-6 rounded-full font-bold text-base sm:text-lg flex items-center gap-3 sm:gap-4 transition-all hover:bg-luby-gold hover:text-white shadow-xl">
          Falar com a nossa equipe
          <span class="w-6 h-6 sm:w-7 sm:h-7 md:w-8 md:h-8 rounded-full bg-white text-black flex items-center justify-center text-sm sm:text-base">
            →
          </span>
        </a>
        <p class="mt-4 sm:mt-6 text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-widest">
          O kit inicial é uma curadoria exclusiva para garantir seu sucesso
        </p>
      </div>

    </div>
  </section>
</template>

<style scoped>
.num-val {
  -webkit-background-clip: text;
  background-clip: text;
  transition: all 0.5s ease;
}
</style>