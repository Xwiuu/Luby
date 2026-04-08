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
    q: "Como funciona a consignação Luby?",
    a: "É o nosso voto de confiança em você. Nós investimos no estoque das semijoias e você investe seu talento. Você recebe o mostruário, tem até 35 dias para realizar as vendas e só paga pelo que efetivamente vender. Risco zero para começar seu negócio."
  },
  {
    q: "Posso escolher as peças do meu primeiro kit?",
    a: "O primeiro kit é uma curadoria estratégica feita por nossas especialistas. Nós selecionamos as semijoias que possuem maior giro e aceitação no mercado para garantir que você tenha lucro imediato e uma excelente primeira experiência de vendas."
  },
  {
    q: "Qual é a minha margem de lucro?",
    a: "Trabalhamos com um sistema de comissões que valoriza seu crescimento. Suas margens começam em 20% e podem chegar a 50% conforme seu volume de vendas. Quanto mais você brilha, mais a Luby te premia."
  },
  {
    q: "As semijoias possuem garantia?",
    a: "Com certeza. Todas as nossas peças são banhadas com tecnologia de ponta em Ouro 18k/24k ou Prata 925 e possuem garantia total contra defeitos de fabricação. Qualidade premium para você encantar suas clientes."
  },
  {
    q: "Preciso ter experiência ou CNPJ?",
    a: "Não é necessário. Você pode iniciar sua jornada com seu CPF. Além disso, nós fornecemos todo o material de apoio, fotos profissionais e suporte para que, mesmo sem experiência, você se torne uma revendedora de sucesso."
  }
]

onMounted(() => {
  // Animação de entrada sutil
  gsap.from(".faq-item", {
    opacity: 0,
    y: 20,
    stagger: 0.1,
    duration: 0.8,
    scrollTrigger: {
      trigger: ".faq-container",
      start: "top 80%"
    }
  })
})
</script>

<template>
  <section id="faq" class="relative bg-[#FFFBF9] py-20 sm:py-24 md:py-32 overflow-hidden z-10 rounded-t-[4rem] -mt-20">
    
    <div class="max-w-6xl mx-auto px-4 sm:px-6 relative z-10">
      
      <div class="flex flex-col lg:flex-row gap-12 sm:gap-16 md:gap-20">
        
        <div class="lg:w-1/3">
          <div class="sticky top-40">
            <span class="text-luby-gold font-mono text-[10px] sm:text-xs tracking-[0.4em] uppercase mb-4 sm:mb-6 block">Transparência</span>
            <h2 class="text-3xl sm:text-4xl md:text-5xl font-brielle text-gray-900 leading-tight">
              Dúvidas <br>
              <span class="text-[#F4C2C2] italic font-light">Frequentes.</span>
            </h2>
            <p class="mt-6 sm:mt-8 text-gray-500 font-sans text-sm sm:text-base leading-relaxed">
              Queremos que você comece com total segurança. Se ainda tiver alguma pergunta, nossa equipe está pronta para te ouvir.
            </p>
          </div>
        </div>

        <div class="lg:w-2/3 faq-container">
          <div 
            v-for="(item, i) in faqs" 
            :key="i"
            class="faq-item border-b border-[#F4C2C2]/20 group"
          >
            <button 
              @click="toggleFaq(i)"
              class="w-full py-6 sm:py-8 md:py-10 flex items-start justify-between text-left transition-all duration-500"
            >
              <div class="flex gap-4 sm:gap-6 md:gap-8 items-start">
                <span class="text-luby-gold font-mono text-xs sm:text-sm mt-1 sm:mt-2 opacity-40 group-hover:opacity-100">0{{ i + 1 }}</span>
                <h3 class="text-lg sm:text-xl md:text-2xl font-brielle text-gray-800 group-hover:text-luby-gold transition-colors">
                  {{ item.q }}
                </h3>
              </div>
              
              <div class="mt-1 sm:mt-2 transition-transform duration-500" :class="{ 'rotate-180 text-luby-gold': activeIndex === i, 'text-gray-300': activeIndex !== i }">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="m6 9 6 6 6-6"/></svg>
              </div>
            </button>

            <div 
              class="grid transition-all duration-500 ease-in-out overflow-hidden"
              :class="activeIndex === i ? 'grid-rows-[1fr] opacity-100 pb-6 sm:pb-8 md:pb-10' : 'grid-rows-[0fr] opacity-0'"
            >
              <div class="min-h-0 pl-12 sm:pl-14 md:pl-16">
                <p class="text-gray-500 text-sm sm:text-base md:text-lg font-sans leading-relaxed max-w-xl">
                  {{ item.a }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="mt-16 sm:mt-20 md:mt-32 p-6 sm:p-8 md:p-10 bg-white rounded-4xl border border-[#F4C2C2]/20 flex flex-col md:flex-row items-center justify-between gap-6 sm:gap-8 shadow-sm hover:shadow-md transition-shadow">
        <div class="flex items-center gap-4 sm:gap-6">
            <div class="w-12 h-12 sm:w-14 sm:h-14 md:w-16 md:h-16 bg-[#FFF5F2] text-[#F4C2C2] rounded-full flex items-center justify-center text-xl sm:text-2xl md:text-3xl shadow-inner">
                🌸
            </div>
            <div>
                <h4 class="text-lg sm:text-xl font-bold text-gray-900">Ainda tem alguma dúvida?</h4>
                <p class="text-gray-500 text-sm sm:text-base">Nossa Equipe esta online para te ajudar agora.</p>
            </div>
        </div>
        <a href="https://wa.me/555484249459?text=Ol%C3%A1!%20Tenho%20algumas%20d%C3%BAvidas%20sobre%20a%20revenda%20da%20Luby." target="_blank" class="bg-[#1A1A1A] text-white px-6 sm:px-8 md:px-10 py-3 sm:py-4 md:py-5 rounded-full font-bold text-sm sm:text-base hover:bg-luby-gold transition-colors flex items-center gap-2 sm:gap-3 shadow-lg">
            Fale com a nossa equipe
            <span class="text-lg sm:text-xl">→</span>
        </a>
      </div>

    </div>
  </section>
</template>

<style scoped>
.grid-rows-\[1fr\] { grid-template-rows: 1fr; }
.grid-rows-\[0fr\] { grid-template-rows: 0fr; }
.font-brielle { letter-spacing: -0.01em; }
</style>