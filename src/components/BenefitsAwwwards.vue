<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  gsap.from(".benefit-card", {
    y: 30,
    opacity: 0,
    duration: 0.8,
    stagger: 0.1,
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".benefits-grid",
      start: "top 85%",
    }
  })
})
</script>

<template>
  <section class="relative z-20 bg-[#FFF8F1] pt-24 pb-32 rounded-t-[3rem] overflow-hidden">
    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="text-center max-w-2xl mx-auto mb-16">
        <span class="inline-flex items-center justify-center px-4 py-1 rounded-full bg-luby-gold/10 text-xs uppercase tracking-[0.35em] text-luby-gold mb-6">Benefícios exclusivos</span>
        <h2 class="text-4xl md:text-6xl font-brielle text-gray-900 leading-tight">
          A excelência Luby <br>
          <span class="text-luby-gold italic font-light">em cada detalhe.</span>
        </h2>
        <p class="mt-6 text-gray-600 text-sm sm:text-base leading-relaxed">
          Descubra propostas criativas e práticas para quem vende sem perder o brilho.
        </p>
      </div>

      <div class="benefits-grid grid grid-cols-1 md:grid-cols-12 gap-6 sm:gap-8">
        <div class="benefit-card md:col-span-7 group relative rounded-[2.5rem] bg-white border border-gray-100 overflow-hidden flex flex-col justify-end min-h-[360px] sm:min-h-[420px] shadow-[0_28px_80px_rgba(15,23,42,0.08)] transition-all duration-500 hover:-translate-y-1">
          <img src="../assets/qualidade.jpeg" alt="Detalhe dourado de joia Luby" class="absolute inset-0 w-full h-full object-cover object-center transition-transform duration-700 group-hover:scale-105">
          <div class="absolute inset-0 bg-gradient-to-t from-black/85 via-black/20 to-transparent"></div>
          <div class="relative z-10 p-6 sm:p-8 lg:p-10 text-white">
            <span class="inline-block mb-4 text-[10px] uppercase tracking-[0.3em] text-white/70">Acabamento Premium</span>
            <h3 class="text-3xl sm:text-4xl font-brielle mb-4">Qualidade Premium</h3>
            <p class="text-white/75 text-sm sm:text-base max-w-full sm:max-w-lg leading-relaxed">
              Banho em Ouro 18k com proteção antialérgica e acabamento impecável para durabilidade e confiança em cada peça.
            </p>
          </div>
        </div>

        <div class="benefit-card md:col-span-5 group relative rounded-[2.5rem] bg-[#F4C2C2] p-6 sm:p-8 lg:p-10 flex flex-col justify-between min-h-[340px] sm:min-h-[420px] shadow-2xl shadow-[#F4C2C2]/20 border border-white/40 transition-all duration-500 hover:-translate-y-1">
          <div class="w-14 h-14 sm:w-16 sm:h-16 rounded-full bg-white/20 flex items-center justify-center text-white backdrop-blur-md">
            <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect width="20" height="14" x="2" y="5" rx="2"/><line x1="2" y1="10" y2="10"/></svg>
          </div>
          <div class="text-white mt-6 sm:mt-0">
            <h3 class="text-2xl sm:text-3xl font-brielle mb-3 italic">Consignado de Verdade.</h3>
            <p class="text-white/85 text-sm sm:text-base leading-relaxed">
              Receba as semijoias e só pague o que vender, com processos simples, sem antecipação e apoio em cada etapa.
            </p>
          </div>
        </div>

        <div class="benefit-card md:col-span-5 group relative rounded-[2.5rem] bg-white border border-gray-100 overflow-hidden min-h-[320px] sm:min-h-[360px] shadow-lg transition-all duration-500 hover:-translate-y-1">
          <img src="../assets/Prata.png" alt="Coleção de semijoias Prata 925 em destaque" class="absolute inset-0 w-full h-full object-cover object-center opacity-90 group-hover:opacity-100 transition-all duration-500">
          <div class="absolute top-8 left-8">
            <span class="bg-gray-950 text-white text-[10px] px-3 py-1 rounded-full uppercase tracking-widest">Coleção Prata 925</span>
          </div>
        </div>

        <div class="benefit-card md:col-span-7 group relative rounded-[2.5rem] bg-[#1A1A1A] p-6 sm:p-8 lg:p-10 flex flex-col md:flex-row items-start md:items-center min-h-[360px] shadow-2xl shadow-black/20 transition-all duration-500 hover:-translate-y-1">
          <div class="flex flex-col sm:flex-row gap-6 sm:gap-8 items-start md:items-center">
            <div class="w-20 h-20 sm:w-24 sm:h-24 rounded-full bg-luby-gold/10 border border-luby-gold/20 flex items-center justify-center text-luby-gold flex-shrink-0">
              <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
            </div>
            <div class="text-white">
              <h3 class="text-2xl sm:text-3xl font-brielle mb-2 text-luby-gold">Apoio em cada venda</h3>
              <p class="text-gray-400 text-sm md:text-base leading-relaxed max-w-full sm:max-w-md">
                Fotos profissionais para Instagram, catálogo digital atualizado e treinamento de vendas exclusivos para você atender clientes com mais confiança.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>