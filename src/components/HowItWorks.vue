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
  <section ref="sectionRef" class="relative bg-[#FFF5F2] pt-20 pb-16 sm:pt-24 sm:pb-20 md:pt-32 md:pb-32 z-10 rounded-t-[3rem] shadow-[0_-20px_50px_rgba(244,194,194,0.1)] -mt-10">
    <div class="max-w-7xl mx-auto px-6 sm:px-8 flex flex-col md:flex-row gap-10 md:gap-16 relative">
      
      <div ref="leftColumnRef" class="md:w-5/12 h-fit md:h-screen flex flex-col justify-center pt-8 md:pt-0 mx-auto md:mx-0 max-w-3xl md:max-w-none">
        <div class="inline-flex items-center gap-3 mb-6">
          <span class="w-8 h-px bg-luby-gold"></span>
          <span class="text-luby-gold font-mono text-xs tracking-[0.2em] uppercase">Sua Evolução</span>
        </div>
        
        <h2 class="text-4xl md:text-5xl lg:text-6xl font-brielle text-gray-900 leading-tight mb-6">
          A jornada para <br>
          <span class="text-luby-gold italic font-light">brilhar com a Luby.</span>
        </h2>
        
        <p class="text-gray-500 font-sans text-base md:text-lg leading-relaxed mb-8 max-w-full sm:max-w-xl">
          Criamos um processo fluido para que você foque apenas no que importa: <span class="text-gray-900 font-medium">encantar e lucrar</span>.
        </p>

        <div class="hidden md:block w-px h-32 bg-gray-200 relative overflow-hidden mt-8 ml-2">
          <div class="absolute top-0 left-0 w-full h-full bg-luby-gold origin-top animate-[scaleY_2s_ease-in-out_infinite_alternate]"></div>
        </div>
      </div>

      <div class="md:w-7/12 flex flex-col gap-10 md:gap-20 pt-8 md:pt-[15vh] pb-12 md:pb-[20vh]">
        
        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-[#F4C2C2] font-mono text-4xl sm:text-5xl md:text-7xl font-bold mb-4 block">01</span>
          <h3 class="text-2xl md:text-3xl font-brielle text-gray-900 mb-4">Curadoria de Perfil</h3>
          <p class="text-gray-500 font-sans text-base md:text-lg leading-relaxed max-w-full md:max-w-md">
            O primeiro passo é um breve cadastro. Nossa equipe analisa seu perfil com carinho para garantir que você tenha a melhor experiência como consultora de <strong class="text-gray-800">semijoias</strong>.
          </p>
        </div>

        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-[#F4C2C2] font-mono text-4xl sm:text-5xl md:text-7xl font-bold mb-4 block">02</span>
          <h3 class="text-2xl md:text-3xl font-brielle text-gray-900 mb-6">Receba seu Acervo</h3>
          
          <div class="relative w-full aspect-video rounded-3xl overflow-hidden mb-8 shadow-xl border-4 border-white">
            <img src="../assets/How.png" alt="Mostruário Luby" class="w-full h-full object-cover">
          </div>

          <p class="text-gray-500 font-sans text-base md:text-lg leading-relaxed max-w-full md:max-w-md">
            Você recebe em casa um kit estratégico montado por nossas especialistas. Peças selecionadas para garantir que você realize suas primeiras vendas já na primeira semana.
          </p>
        </div>

        <div class="step-item opacity-20 scale-95 transition-all duration-500 origin-left">
          <span class="text-[#F4C2C2] font-mono text-4xl sm:text-5xl md:text-7xl font-bold mb-4 block">03</span>
          <h3 class="text-2xl md:text-3xl font-brielle text-gray-900 mb-4">Independência e Brilho</h3>
          <p class="text-gray-500 font-sans text-base md:text-lg leading-relaxed max-w-md">
            Com as semijoias em mãos e nosso material de apoio, você começa a faturar. Lucro de até 50% e a satisfação de empreender com elegância.
          </p>
        </div>

      </div>
    </div>
  </section>
</template>