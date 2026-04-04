<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const activeIndex = ref(0)

const toggleFaq = (index: number) => {
  activeIndex.value = activeIndex.value === index ? -1 : index
}

const faqs = [
  {
    q: "Como funciona a consignação?",
    a: "É simples: nós investimos o estoque, você investe seu talento. Você recebe o mostruário, tem até 35 dias para vender e só paga pelo que sair. Risco zero, lucro real."
  },
  {
    q: "Qual a comissão real que recebo?",
    a: "Trabalhamos com meritocracia. Sua comissão começa em 20% e escala até 50% conforme seu volume de vendas. Quanto mais você brilha, mais a Luby te premia."
  },
  {
    q: "As peças têm garantia?",
    a: "Sim. Nossas semijoias são banhadas a Ouro 18k/24k e Prata 925. Oferecemos garantia total contra defeitos de fábrica e suporte de assistência técnica para suas clientes."
  },
  {
    q: "Preciso de CNPJ ou experiência?",
    a: "Não. Você pode começar com seu CPF. E sobre experiência: nós te entregamos o método e as fotos profissionais. Você só precisa da vontade de crescer."
  },
  {
    q: "Existe um valor mínimo de vendas?",
    a: "Sim, pedimos um giro mínimo de R$ 250,00 por ciclo. É um valor simbólico para garantir que nossa parceria faça sentido para o seu crescimento e para a nossa logística."
  }
]

onMounted(() => {
  // Efeito de Parallax no texto de fundo "FAQ"
  gsap.to(".bg-text-faq", {
    x: -200,
    scrollTrigger: {
      trigger: ".faq-section",
      start: "top bottom",
      end: "bottom top",
      scrub: 2
    }
  })

  // Revelação das perguntas
  gsap.from(".faq-row", {
    opacity: 0,
    y: 30,
    stagger: 0.1,
    duration: 1,
    ease: "power3.out",
    scrollTrigger: {
      trigger: ".faq-list",
      start: "top 80%"
    }
  })
})
</script>

<template>
  <section class="faq-section relative bg-white py-40 overflow-hidden z-10 rounded-t-[4rem] -mt-20">
    
    <div class="bg-text-faq absolute top-20 left-0 whitespace-nowrap pointer-events-none select-none">
      <span class="text-[20vw] font-bold text-gray-100 uppercase leading-none italic" style="-webkit-text-stroke: 1px #e5e7eb; color: transparent;">
        QUESTIONS • QUESTIONS • QUESTIONS •
      </span>
    </div>

    <div class="max-w-6xl mx-auto px-6 relative z-10">
      
      <div class="flex flex-col lg:flex-row gap-20">
        
        <div class="lg:w-1/3">
          <div class="sticky top-40">
            <span class="text-luby-gold font-mono text-sm tracking-[0.3em] uppercase mb-6 block">Suporte Elite</span>
            <h2 class="text-5xl md:text-7xl font-brielle text-gray-950 leading-tight">
              Dúvidas <br>
              <span class="text-gray-400 italic font-light">Frequentes.</span>
            </h2>
            <p class="mt-8 text-gray-500 font-sans leading-relaxed">
              Transparência é a base da nossa parceria. Se não encontrar o que busca, nosso suporte humano está a um clique de distância.
            </p>
          </div>
        </div>

        <div class="lg:w-2/3 faq-list">
          <div 
            v-for="(item, i) in faqs" 
            :key="i"
            class="faq-row border-b border-gray-100 group"
          >
            <button 
              @click="toggleFaq(i)"
              class="w-full py-10 flex items-start justify-between text-left transition-all duration-500 group-hover:pl-4"
            >
              <div class="flex gap-8 items-start">
                <span class="text-luby-gold font-mono text-sm mt-2 opacity-50 group-hover:opacity-100 transition-opacity">0{{ i + 1 }}</span>
                <h3 class="text-2xl md:text-3xl font-brielle text-gray-900 group-hover:text-luby-gold transition-colors duration-300">
                  {{ item.q }}
                </h3>
              </div>
              
              <div class="mt-2 transition-transform duration-500" :class="{ 'rotate-180 text-luby-gold': activeIndex === i, 'text-gray-300': activeIndex !== i }">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m6 9 6 6 6-6"/></svg>
              </div>
            </button>

            <div 
              class="grid transition-all duration-500 ease-in-out overflow-hidden"
              :class="activeIndex === i ? 'grid-rows-[1fr] opacity-100 pb-10' : 'grid-rows-[0fr] opacity-0'"
            >
              <div class="min-h-0 pl-16">
                <p class="text-gray-600 text-lg font-sans leading-relaxed max-w-xl">
                  {{ item.a }}
                </p>
              </div>
            </div>
          </div>
        </div>

      </div>

      <div class="mt-32 p-12 bg-gray-50 rounded-[3rem] border border-gray-100 flex flex-col md:flex-row items-center justify-between gap-8 group hover:bg-white hover:shadow-2xl transition-all duration-500">
        <div class="flex items-center gap-6">
            <div class="w-16 h-16 bg-green-500/10 text-green-600 rounded-full flex items-center justify-center text-3xl">
                💬
            </div>
            <div>
                <h4 class="text-xl font-bold text-gray-900">Ainda tem alguma dúvida específica?</h4>
                <p class="text-gray-500">Fale agora com uma de nossas consultoras pelo WhatsApp.</p>
            </div>
        </div>
        <button class="bg-gray-950 text-white px-10 py-5 rounded-full font-bold hover:bg-green-600 transition-colors flex items-center gap-3">
            Falar com Consultora
            <span class="text-xl">→</span>
        </button>
      </div>

    </div>
  </section>
</template>

<style scoped>
/* Tipografia fina */
.font-brielle {
  letter-spacing: -0.02em;
}

/* Efeito de transição do Grid Rows */
.grid-rows-\[1fr\] {
  grid-template-rows: 1fr;
}
.grid-rows-\[0fr\] {
  grid-template-rows: 0fr;
}
</style>