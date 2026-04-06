<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const leftColumnRef = ref(null)

onMounted(() => {
  const steps = gsap.utils.toArray('.step-item')
  let mm = gsap.matchMedia();

  mm.add("(min-width: 768px)", () => {
    ScrollTrigger.create({
      trigger: sectionRef.value,
      start: "top top",
      end: "bottom bottom",
      pin: leftColumnRef.value,
      pinSpacing: false,
    })
  });

  steps.forEach((step: any) => {
    gsap.to(step, {
      opacity: 1,
      scale: 1,
      scrollTrigger: {
        trigger: step,
        start: "top 75%",
        end: "top 30%",
        scrub: 1,
      }
    })
  })
})
</script>

<template>
  <section ref="sectionRef" class="relative bg-[#FFF5F2] pt-16 sm:pt-20 md:pt-32 pb-12 sm:pb-16 md:pb-32 z-10 rounded-t-[3rem] shadow-[0_-20px_50px_rgba(0,0,0,0.03)] -mt-10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 flex flex-col md:flex-row gap-6 sm:gap-8 md:gap-16 relative">
      
      <div ref="leftColumnRef" class="md:w-5/12 h-fit md:h-screen flex flex-col justify-center pt-4 sm:pt-6 md:pt-0">
        <div class="inline-flex items-center gap-2 sm:gap-3 mb-4 sm:mb-6">
          <span class="w-6 sm:w-8 h-px bg-luby-gold"></span>
          <span class="text-luby-gold font-mono text-[10px] sm:text-xs tracking-[0.2em] uppercase">O Caminho</span>
        </div>
        
        <h2 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-brielle text-[#1A1A1A] leading-tight mb-4 sm:mb-6">
          Três passos para <br>
          o seu <span class="text-luby-gold italic font-light">novo império.</span>
        </h2>
        
        <p class="text-gray-500 font-sans text-sm sm:text-base md:text-lg leading-relaxed mb-6 sm:mb-8 max-w-sm">
          Desenhamos um processo livre de burocracia. Você foca em encantar suas clientes, nós cuidamos de toda a estrutura.
        </p>

        <div class="hidden md:block w-px h-32 bg-gray-200 relative overflow-hidden mt-6 sm:mt-8 ml-2">
          <div class="absolute top-0 left-0 w-full h-full bg-luby-gold origin-top animate-[scaleY_2s_ease-in-out_infinite_alternate]"></div>
        </div>
      </div>

      <div class="md:w-7/12 flex flex-col gap-8 sm:gap-10 md:gap-24 pt-4 sm:pt-6 md:pt-[15vh] pb-8 sm:pb-12 md:pb-[20vh]">
        
        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-[#F4C2C2] font-mono text-4xl sm:text-5xl md:text-7xl font-bold mb-3 sm:mb-4 block">01</span>
          <h3 class="text-xl sm:text-2xl md:text-3xl font-brielle text-[#1A1A1A] mb-3 sm:mb-4">Cadastro de Curadoria</h3>
          <p class="text-gray-500 font-sans text-sm sm:text-base md:text-lg leading-relaxed max-w-md">
            Preencha nosso formulário. Nossa equipe fará uma análise carinhosa para liberar seu acesso ao mundo Luby Semijoias.
          </p>
        </div>

        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-[#F4C2C2] font-mono text-4xl sm:text-5xl md:text-7xl font-bold mb-3 sm:mb-4 block">02</span>
          <h3 class="text-xl sm:text-2xl md:text-3xl font-brielle text-[#1A1A1A] mb-3 sm:mb-4">Receba seu Acervo</h3>
          <p class="text-gray-500 font-sans text-sm sm:text-base md:text-lg leading-relaxed max-w-md">
            Enviamos para você um kit estratégico, com semijoias selecionadas por nossas especialistas para garantir que suas vendas sejam um sucesso imediato.
          </p>
        </div>

        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-[#F4C2C2] font-mono text-4xl sm:text-5xl md:text-7xl font-bold mb-3 sm:mb-4 block">03</span>
          <h3 class="text-xl sm:text-2xl md:text-3xl font-brielle text-[#1A1A1A] mb-3 sm:mb-4">Brilhe e Lucre</h3>
          <p class="text-gray-500 font-sans text-sm sm:text-base md:text-lg leading-relaxed max-w-md">
            Com as semijoias em mãos e nosso suporte exclusivo, você está pronta para conquistar sua independência financeira com elegância.
          </p>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes scaleY {
  0% { transform: scaleY(0); }
  100% { transform: scaleY(1); }
}

.step-item {
  will-change: transform, opacity;
}
</style>