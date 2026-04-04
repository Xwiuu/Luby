<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)

// O Segredo Awwwards: Efeito de luz dinâmica (Glow) que segue o mouse
const handleMouseMove = (e: MouseEvent) => {
  const cards = document.querySelectorAll('.awwwards-card')
  cards.forEach((card: any) => {
    const rect = card.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top
    card.style.setProperty('--mouse-x', `${x}px`)
    card.style.setProperty('--mouse-y', `${y}px`)
  })
}

onMounted(() => {
  // Animação do Título (Surgindo das sombras)
  gsap.from(".benefits-title > *", {
    y: 40,
    opacity: 0,
    duration: 1.2,
    stagger: 0.15,
    ease: "power4.out",
    scrollTrigger: {
      trigger: sectionRef.value,
      start: "top 75%",
    }
  })

  // Entrada dos Cards (Bento Grid) com escala e fade 3D
  gsap.from(".awwwards-card", {
    y: 80,
    opacity: 0,
    scale: 0.95,
    rotationX: 5,
    duration: 1.2,
    stagger: 0.1,
    ease: "expo.out",
    scrollTrigger: {
      trigger: ".bento-grid",
      start: "top 80%",
    }
  })

  // Animação flutuante (Levitação) contínua nos ícones
  gsap.to(".floating-icon", {
    y: -8,
    duration: 2.5,
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
    class="benefits-section relative z-20 bg-[#050505] pt-32 pb-32 -mt-10 rounded-t-[3rem] shadow-[0_-30px_60px_rgba(0,0,0,0.5)] overflow-hidden"
    @mousemove="handleMouseMove"
  >
    <div class="absolute inset-0 opacity-[0.03] pointer-events-none" style="background-image: url('data:image/svg+xml,%3Csvg viewBox=%220 0 200 200%22 xmlns=%22http://www.w3.org/2000/svg%22%3E%3Cfilter id=%22noiseFilter%22%3E%3CfeTurbulence type=%22fractalNoise%22 baseFrequency=%220.65%22 numOctaves=%223%22 stitchTiles=%22stitch%22/%3E%3C/filter%3E%3Crect width=%22100%25%22 height=%22100%25%22 filter=%22url(%23noiseFilter)%22/%3E%3C/svg%3E');"></div>

    <div class="max-w-7xl mx-auto px-6 relative z-10">
      
      <div class="benefits-title text-center max-w-3xl mx-auto mb-24">
        <div class="inline-flex items-center justify-center gap-3 mb-6">
          <span class="h-px w-8 bg-luby-gold/50"></span>
          <span class="text-luby-gold font-mono text-xs tracking-[0.3em] uppercase">O Diferencial Luby</span>
          <span class="h-px w-8 bg-luby-gold/50"></span>
        </div>
        <h2 class="text-5xl md:text-6xl font-brielle text-white leading-tight">
          Padrão de <span class="text-luby-gold italic font-light">excelência</span> <br>
          em cada detalhe.
        </h2>
      </div>

      <div class="bento-grid grid grid-cols-1 md:grid-cols-12 gap-6 auto-rows-[340px]">
        
        <div class="awwwards-card md:col-span-8 group relative rounded-4xl bg-[#0c0c0c] border border-white/5 overflow-hidden p-10 flex flex-col justify-between cursor-default">
          <div class="card-glow absolute inset-0 opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>
          
          <div class="flex justify-between items-start relative z-10">
            <div class="floating-icon w-16 h-16 rounded-2xl bg-luby-gold/10 border border-luby-gold/20 flex items-center justify-center text-luby-gold backdrop-blur-md">
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M6 3h12l4 6-10 13L2 9Z"/><path d="M11 3 8 9l4 13 4-13-3-6"/><path d="M2 9h20"/></svg>
            </div>
            <span class="font-mono text-5xl font-bold text-white/5 group-hover:text-luby-gold/10 transition-colors duration-500">01</span>
          </div>

          <div class="relative z-10 max-w-lg transform group-hover:translate-x-2 transition-transform duration-500">
            <h3 class="text-3xl font-brielle text-white mb-4">Margem de Lucro Elevada</h3>
            <p class="text-gray-400 font-sans leading-relaxed text-sm md:text-base">
              Esqueça a guerra de centavos. Nossas peças possuem design autoral e alto valor percebido, permitindo que você trabalhe com margens que transformam vendas em construção de patrimônio real.
            </p>
          </div>
        </div>

        <div class="awwwards-card md:col-span-4 group relative rounded-4xl bg-gradient-to-br from-[#111] to-[#050505] border border-white/5 overflow-hidden p-10 flex flex-col justify-between cursor-default">
          <div class="card-glow absolute inset-0 opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>
          
          <div class="relative z-10">
            <div class="floating-icon w-14 h-14 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-white mb-8 backdrop-blur-md">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/><path d="M5 3v4"/><path d="M19 17v4"/><path d="M3 5h4"/><path d="M17 19h4"/></svg>
            </div>
            <h3 class="text-2xl font-brielle text-white mb-3">Desejo Imediato</h3>
            <p class="text-gray-400 font-sans text-sm leading-relaxed">
              O design luxuoso faz o produto se vender no primeiro olhar. Menos objeções, mais fechamentos rápidos.
            </p>
          </div>
          
          <div class="absolute bottom-10 right-10 opacity-0 transform translate-x-4 group-hover:opacity-100 group-hover:translate-x-0 transition-all duration-500 text-luby-gold">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
          </div>
        </div>

        <div class="awwwards-card md:col-span-5 group relative rounded-4xl bg-[#F4C2C2] overflow-hidden p-10 flex flex-col justify-between cursor-default">
          <div class="absolute inset-0 bg-gradient-to-t from-black/40 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 z-0"></div>
          
          <div class="relative z-10 flex justify-between items-start">
            <div class="floating-icon w-14 h-14 rounded-full bg-white/40 flex items-center justify-center text-gray-900 shadow-lg backdrop-blur-md">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="14" x="2" y="5" rx="2"/><line x1="2" x2="22" y1="10" y2="10"/></svg>
            </div>
          </div>
          
          <div class="relative z-10">
            <h3 class="text-2xl font-brielle text-gray-900 mb-3">Acesso Facilitado</h3>
            <p class="text-gray-800 font-sans text-sm leading-relaxed">
              Modelo de entrada inteligente. Você não precisa descapitalizar para começar a faturar. O risco é mínimo e o retorno é ágil.
            </p>
          </div>
        </div>

        <div class="awwwards-card md:col-span-7 group relative rounded-4xl bg-[#0c0c0c] border border-white/5 overflow-hidden p-10 flex items-center cursor-default">
          <div class="card-glow absolute inset-0 opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>
          
          <div class="relative z-10 flex flex-col md:flex-row gap-8 items-start md:items-center w-full">
            <div class="floating-icon shrink-0 w-20 h-20 rounded-full border border-luby-gold/30 flex items-center justify-center text-luby-gold relative">
              <div class="absolute inset-0 border border-luby-gold/10 rounded-full animate-ping opacity-20"></div>
              <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
            </div>
            
            <div>
              <h3 class="text-3xl font-brielle text-white mb-3">Suporte & Estrutura</h3>
              <p class="text-gray-400 font-sans text-sm leading-relaxed max-w-md">
                Entregamos a faca e o queijo. Catálogo digital impecável, banco de imagens em altíssima resolução e treinamento focado em vendas. Você só precisa executar.
              </p>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
/* O mágico efeito de Glare/Lanterna acompanhando o mouse */
.awwwards-card {
  position: relative;
}

.awwwards-card::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    800px circle at var(--mouse-x, 0) var(--mouse-y, 0),
    rgba(212, 175, 55, 0.06), /* Brilho Dourado bem sutil */
    transparent 40%
  );
  z-index: 1;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.awwwards-card:hover::before {
  opacity: 1;
}
</style>