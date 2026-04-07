<script setup lang="ts">
import { onMounted, ref, onUnmounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

// 1. Definimos o tipo HTMLElement para o TS não reclamar do null
const containerRef = ref<HTMLElement | null>(null)
const gridRef = ref<HTMLElement | null>(null)
let ctx: gsap.Context

onMounted(() => {
  // 2. Checagem de segurança: Se as refs não existirem, a gente nem tenta rodar
  if (!containerRef.value || !gridRef.value) return

  setTimeout(() => {
    // 3. O 'as HTMLElement' garante ao TS que o valor não é nulo aqui dentro
    ctx = gsap.context(() => {
      const cards = gsap.utils.toArray('.benefit-card')
      
      if (cards.length > 0) {
        gsap.fromTo(cards, 
          { y: 50, opacity: 0 }, 
          {
            y: 0,
            opacity: 1,
            duration: 1,
            stagger: 0.15,
            ease: "power3.out",
            scrollTrigger: {
              trigger: gridRef.value as HTMLElement, // Cast de segurança
              start: "top 85%",
              toggleActions: "play none none none",
              onEnter: () => ScrollTrigger.refresh()
            }
          }
        )
      }
    }, containerRef.value as HTMLElement) // Cast de segurança
    
    ScrollTrigger.refresh()
  }, 100)
})

onUnmounted(() => {
  if (ctx) ctx.revert()
})
</script>

<template>
  <section
    ref="containerRef"
    class="relative z-20 bg-[#FFFBF9] pt-24 pb-32 rounded-t-[3rem] overflow-hidden"
  >
    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="text-center max-w-2xl mx-auto mb-16">
        <span
          class="inline-flex items-center justify-center px-4 py-1 rounded-full bg-luby-gold/10 text-[10px] uppercase tracking-[0.4em] text-luby-gold mb-6"
        >
          Diferenciais Luby
        </span>
        <h2
          class="text-4xl md:text-6xl font-brielle text-gray-900 leading-tight"
        >
          A excelência Luby <br />
          <span class="text-luby-gold italic font-light">em cada detalhe.</span>
        </h2>
      </div>

      <div
        ref="gridRef"
        class="benefits-grid grid grid-cols-1 md:grid-cols-12 gap-6 sm:gap-8 min-h-[600px]"
      >
        <div
          class="benefit-card md:col-span-7 group relative rounded-[2.5rem] bg-white border border-gray-100 overflow-hidden flex flex-col justify-end min-h-[380px] sm:min-h-[450px] shadow-sm transition-all duration-500 hover:-translate-y-1"
        >
          <img
            src="../assets/qualidade.jpeg"
            alt="Qualidade Luby"
            class="absolute inset-0 w-full h-full object-cover"
          />
          <div
            class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent"
          ></div>
          <div class="relative z-10 p-8 sm:p-10 text-white">
            <h3 class="text-3xl sm:text-4xl font-brielle mb-4">
              Qualidade Absoluta
            </h3>
            <p class="text-white/80 text-sm sm:text-base max-w-md">
              Banho em Ouro 18k com proteção antialérgica e acabamento impecável
              de fábrica.
            </p>
          </div>
        </div>

        <div
          class="benefit-card md:col-span-5 group relative rounded-[2.5rem] bg-[#F4C2C2] p-8 sm:p-10 flex flex-col justify-between min-h-[380px] sm:min-h-[450px] shadow-xl shadow-[#F4C2C2]/10 transition-all duration-500"
        >
          <div
            class="w-16 h-16 rounded-full bg-white/20 flex items-center justify-center text-white backdrop-blur-md"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="32"
              height="32"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.5"
            >
              <rect width="20" height="14" x="2" y="5" rx="2" />
              <line x1="2" y1="10" y2="10" />
            </svg>
          </div>
          <div class="text-white">
            <h3 class="text-2xl sm:text-3xl font-brielle mb-3 italic">
              Consignado de Verdade.
            </h3>
            <p class="text-white/90 text-sm leading-relaxed">
              Só pague o que vender. Modelo de risco zero para você focar no seu
              crescimento.
            </p>
          </div>
        </div>

        <div
          class="benefit-card md:col-span-5 group relative rounded-[2.5rem] bg-white border border-gray-100 overflow-hidden min-h-[320px] sm:min-h-[380px] shadow-sm transition-all duration-500"
        >
          <img
            src="../assets/Prata.png"
            alt="Produção Luby"
            class="absolute inset-0 w-full h-full object-cover opacity-90"
          />
          <div class="absolute top-8 left-8">
            <span
              class="bg-luby-gold text-white text-[10px] px-3 py-1 rounded-full uppercase tracking-widest font-bold"
              >Galvânica Própria</span
            >
          </div>
        </div>

        <div
          class="benefit-card md:col-span-7 group relative rounded-[2.5rem] bg-[#1A1A1A] p-8 sm:p-10 flex flex-col md:flex-row items-center min-h-[320px] sm:min-h-[380px] shadow-2xl transition-all duration-500"
        >
          <div class="flex flex-col sm:flex-row gap-8 items-center">
            <div
              class="w-20 h-20 rounded-full bg-luby-gold/10 border border-luby-gold/20 flex items-center justify-center text-luby-gold shrink-0"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="36"
                height="36"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="1.2"
              >
                <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z" />
              </svg>
            </div>
            <div class="text-white text-center sm:text-left">
              <h3 class="text-2xl sm:text-3xl font-brielle mb-2 text-luby-gold">
                Agilidade Total
              </h3>
              <p
                class="text-gray-400 text-sm sm:text-base leading-relaxed max-w-sm"
              >
                Lançamentos semanais e suporte direto da fábrica para consertos
                rápidos e garantia.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Evita que o GSAP esconda os elementos permanentemente se o JS travar */
.benefit-card {
  will-change: transform, opacity;
}
</style>
