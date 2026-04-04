<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const leftColumnRef = ref(null)

onMounted(() => {
  const steps = gsap.utils.toArray('.step-item')

  // Criamos um contexto para lidar com diferentes tamanhos de tela
  let mm = gsap.matchMedia();

  mm.add("(min-width: 768px)", () => {
    // ESTA PARTE SÓ RODA NO DESKTOP (MD para cima)
    ScrollTrigger.create({
      trigger: sectionRef.value,
      start: "top top",
      end: "bottom bottom",
      pin: leftColumnRef.value,
      pinSpacing: false,
    })
  });

  // ESTA PARTE RODA EM TUDO (MOBILE E DESKTOP)
  steps.forEach((step: any) => {
    gsap.to(step, {
      opacity: 1,
      scale: 1,
      scrollTrigger: {
        trigger: step,
        start: "top 75%", // Ajustado um pouco para o mobile "acender" mais cedo
        end: "top 30%",
        scrub: 1,
        toggleClass: "active-step"
      }
    })
  })
})
</script>

<template>
  <section ref="sectionRef" class="relative bg-luby-nude pt-20 pb-16 md:pt-32 md:pb-32 z-10 rounded-t-[3rem] shadow-[0_-20px_50px_rgba(0,0,0,0.1)] -mt-10">
    <div class="max-w-7xl mx-auto px-6 flex flex-col md:flex-row gap-8 md:gap-16 relative">
      
      <div ref="leftColumnRef" class="md:w-5/12 h-fit md:h-screen flex flex-col justify-center pt-8 md:pt-0">
        <div class="inline-flex items-center gap-3 mb-6">
          <span class="w-8 h-px bg-gray-900"></span>
          <span class="text-gray-900 font-mono text-xs tracking-[0.2em] uppercase">A Jornada</span>
        </div>
        
        <h2 class="text-4xl md:text-5xl lg:text-6xl font-brielle text-gray-950 leading-tight mb-6">
          Três passos para <br>
          o seu <span class="text-luby-gold italic font-light">novo império.</span>
        </h2>
        
        <p class="text-gray-600 font-sans text-base md:text-lg leading-relaxed mb-8 max-w-sm">
          Desenhamos um processo livre de burocracia. Você foca em vender e encantar, nós cuidamos de toda a estrutura por trás.
        </p>

        <div class="hidden md:block w-px h-32 bg-gray-300 relative overflow-hidden mt-8 ml-2">
          <div class="absolute top-0 left-0 w-full h-full bg-luby-gold origin-top animate-[scaleY_2s_ease-in-out_infinite_alternate]"></div>
        </div>
      </div>

      <div class="md:w-7/12 flex flex-col gap-12 md:gap-24 pt-8 md:pt-[15vh] pb-16 md:pb-[20vh]">
        
        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-luby-gold font-mono text-5xl md:text-7xl font-bold opacity-30 mb-4 block">01</span>
          <h3 class="text-2xl md:text-3xl font-brielle text-gray-950 mb-4">Cadastro Exclusivo</h3>
          <p class="text-gray-600 font-sans text-base md:text-lg leading-relaxed max-w-md">
            Preencha nosso formulário rápido. Nossa equipe fará uma curadoria ágil para garantir que você tenha o perfil ideal e liberar seu acesso ao portal de revendedoras.
          </p>
        </div>

        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-luby-gold font-mono text-5xl md:text-7xl font-bold opacity-30 mb-4 block">02</span>
          <h3 class="text-2xl md:text-3xl font-brielle text-gray-950 mb-4">Receba seu Acervo</h3>
          <p class="text-gray-600 font-sans text-base md:text-lg leading-relaxed max-w-md">
            Escolha seu kit inicial com peças selecionadas a dedo pelas nossas especialistas, ou monte seu próprio mostruário de acordo com o perfil das suas clientes.
          </p>
        </div>

        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-luby-gold font-mono text-5xl md:text-7xl font-bold opacity-30 mb-4 block">03</span>
          <h3 class="text-2xl md:text-3xl font-brielle text-gray-950 mb-4">Lucre com Elegância</h3>
          <p class="text-gray-600 font-sans text-base md:text-lg leading-relaxed max-w-md">
            Com as joias em mãos e acesso ao nosso material de marketing de alta conversão, você já está pronta para começar a faturar na primeira semana.
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

/* Otimização para performance em dispositivos móveis */
.step-item {
  will-change: transform, opacity;
}
</style>