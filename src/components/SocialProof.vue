<script setup lang="ts">
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const reviewsRow1 = [
  { name: "Mariana S.", result: "R$ 4.200 no 1º mês", text: "Nunca tinha vendido nada na vida. As peças chegaram, postei no Instagram e em 3 dias recuperei o investimento." },
  { name: "Camila T.", result: "Independência", text: "A qualidade da Luby é surreal. Minhas clientes da antiga marca que eu revendia migraram todas pra cá." },
  { name: "Letícia B.", result: "Lucro Real", text: "O que eu mais gosto é não precisar dar desconto. A joia se vende pela apresentação e pelo brilho." },
]

const reviewsRow2 = [
  { name: "Juliana R.", result: "Suporte VIP", text: "O catálogo e as fotos prontas economizam 90% do meu tempo. É só disparar no WhatsApp e anotar os pedidos." },
  { name: "Patrícia V.", result: "Virada de Chave", text: "Eu tinha medo de ficar com estoque parado. A curadoria delas é tão boa que falta produto na minha mão!" },
  { name: "Beatriz C.", result: "Status", text: "Não é só dinheiro, é como a gente se sente vendendo algo tão chique. Orgulho demais." },
]

const duplicatedRow1 = [...reviewsRow1, ...reviewsRow1, ...reviewsRow1]
const duplicatedRow2 = [...reviewsRow2, ...reviewsRow2, ...reviewsRow2]

onMounted(() => {
  gsap.from(".proof-header > *", {
    y: 40, opacity: 0, duration: 1, stagger: 0.15, ease: "power3.out",
    scrollTrigger: { trigger: ".proof-section", start: "top 80%" }
  })

  // Animação das notificações do WhatsApp subindo e aparecendo
  gsap.from(".whatsapp-notif", {
    y: 50, opacity: 0, duration: 0.8, stagger: 0.3, ease: "back.out(1.5)",
    scrollTrigger: { trigger: ".proof-visual", start: "top 70%" }
  })
})
</script>

<template>
  <section class="proof-section relative bg-white py-32 overflow-hidden z-10 rounded-t-[3rem] shadow-[0_-20px_50px_rgba(0,0,0,0.05)] -mt-10">
    <div class="absolute top-0 right-0 w-125 h-125 bg-luby-rose/20 rounded-full blur-[100px] pointer-events-none -translate-y-1/2 translate-x-1/3"></div>

    <div class="max-w-7xl mx-auto px-6 relative z-10 mb-24 flex flex-col lg:flex-row lg:items-center justify-between gap-16">
      
      <div class="proof-header max-w-xl">
        <div class="inline-flex items-center gap-2 mb-6">
          <span class="flex h-3 w-3 relative">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
            <span class="relative inline-flex rounded-full h-3 w-3 bg-green-500"></span>
          </span>
        </div>
        
        <h2 class="text-5xl md:text-6xl font-brielle text-gray-900 leading-tight mb-8">
          Histórias reais de <br>
          <span class="text-luby-gold italic font-light">transformação.</span>
        </h2>

        <div class="flex items-center gap-4 bg-gray-50 px-6 py-4 rounded-2xl border border-gray-100 shadow-sm w-fit">
          <div class="text-4xl font-bold text-gray-900 font-brielle">4.9</div>
          <div class="flex flex-col">
            <div class="flex text-luby-gold text-lg mb-1">★★★★★</div>
            <span class="text-xs font-mono text-gray-500 uppercase tracking-wider">Média de satisfação</span>
          </div>
        </div>
      </div>

      <div class="proof-visual relative w-full lg:w-5/12 h-75 flex flex-col justify-center items-center lg:items-end">
        <div class="absolute inset-0 bg-linear-to-tr from-luby-nude/40 to-transparent rounded-[3rem] transform rotate-3"></div>
        
        <div class="whatsapp-notif relative z-10 bg-white/90 backdrop-blur-md p-4 rounded-2xl shadow-[0_10px_40px_rgba(0,0,0,0.08)] border border-gray-100 flex items-center gap-4 w-[90%] md:w-95 mb-4 transform -translate-x-4">
          <div class="w-12 h-12 rounded-full bg-green-100 flex items-center justify-center shrink-0">
            <span class="text-2xl">💰</span>
          </div>
          <div>
            <div class="flex items-center gap-2">
              <span class="font-bold text-gray-900 text-sm">Carol Revendedora</span>
              <span class="text-[10px] text-gray-400">Agora mesmo</span>
            </div>
            <p class="text-gray-600 text-sm leading-snug">Menina, as clientes tão loucas! Vendi 3 colares no almoço 😱</p>
          </div>
        </div>

        <div class="whatsapp-notif relative z-10 bg-white/90 backdrop-blur-md p-4 rounded-2xl shadow-[0_10px_40px_rgba(0,0,0,0.08)] border border-gray-100 flex items-center gap-4 w-[90%] md:w-95 transform translate-x-4">
          <div class="w-12 h-12 rounded-full bg-luby-rose flex items-center justify-center shrink-0">
            <span class="text-2xl">✨</span>
          </div>
          <div>
            <div class="flex items-center gap-2">
              <span class="font-bold text-gray-900 text-sm">Suporte Luby</span>
              <span class="text-[10px] text-gray-400">2 min atrás</span>
            </div>
            <p class="text-gray-600 text-sm leading-snug">Seu novo kit de reposição já foi despachado! 📦🚀</p>
          </div>
        </div>
      </div>
    </div>

    <div class="relative flex flex-col gap-6 mt-12">
      <div class="absolute inset-y-0 left-0 w-12 md:w-32 bg-linear-to-r from-white to-transparent z-20 pointer-events-none"></div>
      <div class="absolute inset-y-0 right-0 w-12 md:w-32 bg-linear-to-l from-white to-transparent z-20 pointer-events-none"></div>

      <div class="marquee-container flex w-max">
        <div class="marquee-content-left flex gap-6 px-3">
          <div v-for="(review, index) in duplicatedRow1" :key="'row1-'+index" class="w-75 md:w-100 p-8 rounded-4xl bg-luby-nude/30 border border-[#F4C2C2]/50 hover:bg-luby-nude/60 transition-colors duration-300 shrink-0">
            <div class="flex justify-between items-start mb-6">
              <div>
                <h4 class="font-bold text-gray-900 font-sans text-lg">{{ review.name }}</h4>
                <p class="text-luby-gold font-mono text-xs uppercase tracking-wider mt-1">{{ review.result }}</p>
              </div>
            </div>
            <p class="text-gray-600 font-sans leading-relaxed text-sm md:text-base">{{ review.text }}</p>
          </div>
        </div>
      </div>

      <div class="marquee-container flex w-max">
        <div class="marquee-content-right flex gap-6 px-3">
          <div v-for="(review, index) in duplicatedRow2" :key="'row2-'+index" class="w-75 md:w-100 p-8 rounded-4xl bg-gray-50 border border-gray-100 hover:bg-gray-100 transition-colors duration-300 shrink-0">
            <div class="flex justify-between items-start mb-6">
              <div>
                <h4 class="font-bold text-gray-900 font-sans text-lg">{{ review.name }}</h4>
                <p class="text-luby-gold font-mono text-xs uppercase tracking-wider mt-1">{{ review.result }}</p>
              </div>
            </div>
            <p class="text-gray-600 font-sans leading-relaxed text-sm md:text-base">{{ review.text }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.marquee-content-left { animation: scrollLeft 40s linear infinite; }
.marquee-content-right { animation: scrollRight 40s linear infinite; }
.marquee-container:hover .marquee-content-left, .marquee-container:hover .marquee-content-right { animation-play-state: paused; }
@keyframes scrollLeft { 0% { transform: translateX(0); } 100% { transform: translateX(-33.33%); } }
@keyframes scrollRight { 0% { transform: translateX(-33.33%); } 100% { transform: translateX(0); } }
</style>