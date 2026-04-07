<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)

onMounted(() => {
  gsap.from(".story-content > *", {
    y: 40,
    opacity: 0,
    duration: 1.2,
    stagger: 0.2,
    ease: "power3.out",
    scrollTrigger: {
      trigger: sectionRef.value,
      start: "top 70%",
    }
  })
})
</script>

<template>
  <section ref="sectionRef" class="relative bg-white py-32 overflow-hidden">
    <div class="max-w-7xl mx-auto px-6">
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 items-center">
        
        <div class="lg:col-span-5 relative">
          <div class="aspect-[4/5] rounded-[3rem] overflow-hidden shadow-2xl border-8 border-[#FFF5F2]">
            <img src="../assets/founder.jpeg" alt="Fundadora Luby" class="w-full h-full object-cover">
          </div>
          <div class="absolute -bottom-10 -right-6 bg-[#1A1A1A] text-white p-8 rounded-3xl max-w-[240px] shadow-xl">
            <p class="font-brielle text-lg leading-tight mb-2">"Persistência constrói a vida que você merece."</p>
            <p class="text-[10px] font-mono uppercase tracking-widest text-luby-gold">Nossa Fundadora</p>
          </div>
        </div>

        <div class="lg:col-span-7 story-content">
          <div class="inline-flex items-center gap-3 mb-6">
            <span class="w-10 h-px bg-luby-gold"></span>
            <span class="text-luby-gold font-mono text-xs tracking-[0.4em] uppercase">Nossa Essência</span>
          </div>
          
          <h2 class="text-4xl md:text-6xl font-brielle text-gray-950 mb-10 leading-tight">
            Mais do que semijoias, <br>
            <span class="text-luby-gold italic font-light">construímos histórias.</span>
          </h2>

          <div class="space-y-6 text-gray-600 text-lg leading-relaxed font-light">
            <p>
              A Luby nasceu com um propósito claro: <span class="text-gray-900 font-medium italic">transformar vidas através da beleza e da oportunidade.</span>
            </p>
            <p>
              Acreditamos que cada revendedora carrega um sonho. Por isso, oferecemos mais do que produtos — entregamos suporte verdadeiro, orientação e um caminho estruturado para o crescimento financeiro.
            </p>
            <p>
              Nossa essência está na qualidade absoluta e no cuidado com quem faz parte dessa rede de mulheres fortes e determinadas que decidiram crescer juntas.
            </p>
          </div>

          <div class="mt-12 pt-8 border-t border-gray-100">
             <p class="font-brielle text-2xl text-gray-900 italic">Luby. Feita para brilhar — dentro e fora de você.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>