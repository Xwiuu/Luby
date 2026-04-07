<script setup lang="ts">
import { onMounted, ref, onUnmounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

// Refs para garantir estabilidade no Deploy (Vite/TS)
const containerRef = ref<HTMLElement | null>(null);
const gridRef = ref<HTMLElement | null>(null);
let ctx: gsap.Context;

onMounted(() => {
  if (!containerRef.value || !gridRef.value) return;

  setTimeout(() => {
    ctx = gsap.context(() => {
      const cards = gsap.utils.toArray(".benefit-card");

      if (cards.length > 0) {
        gsap.fromTo(
          cards,
          { y: 40, opacity: 0 },
          {
            y: 0,
            opacity: 1,
            duration: 1,
            stagger: 0.12,
            ease: "power3.out",
            scrollTrigger: {
              trigger: gridRef.value as HTMLElement,
              start: "top 85%",
              toggleActions: "play none none none",
            },
          },
        );
      }
    }, containerRef.value as HTMLElement);

    ScrollTrigger.refresh();
  }, 100);
});

onUnmounted(() => {
  if (ctx) ctx.revert();
});
</script>

<template>
  <section
    ref="containerRef"
    class="relative z-20 bg-[#FFFBF9] pt-24 pb-32 rounded-t-[3rem] overflow-hidden"
  >
    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="text-center max-w-2xl mx-auto mb-16">
        <span
          class="inline-flex items-center justify-center px-4 py-1 rounded-full bg-luby-gold/10 text-[10px] uppercase tracking-[0.35em] text-luby-gold mb-6"
          >Excelência & Autoridade</span
        >
        <h2
          class="text-4xl md:text-6xl font-brielle text-gray-900 leading-tight"
        >
          A estrutura Luby <br />
          <span class="text-luby-gold italic font-light">em cada detalhe.</span>
        </h2>
      </div>

      <div
        ref="gridRef"
        class="benefits-grid grid grid-cols-1 md:grid-cols-12 gap-6 sm:gap-8"
      >
        <div
          class="benefit-card md:col-span-7 group relative rounded-[2.5rem] bg-white border border-gray-100 overflow-hidden flex flex-col justify-end min-h-[380px] sm:min-h-[450px] shadow-lg transition-all duration-500 hover:-translate-y-1"
        >
          <img
            src="../assets/qualidade.jpeg"
            alt="Qualidade Luby"
            class="absolute inset-0 w-full h-full object-cover object-center transition-transform duration-700 group-hover:scale-105"
          />
          <div
            class="absolute inset-0 bg-gradient-to-t from-black/85 via-black/10 to-transparent"
          ></div>
          <div class="relative z-10 p-8 sm:p-10 text-white">
            <span
              class="inline-block mb-2 text-[10px] uppercase tracking-[0.3em] text-white/70 font-mono"
              >Padrão Ouro</span
            >
            <h3 class="text-3xl sm:text-4xl font-brielle mb-4">
              Qualidade Absoluta
            </h3>
            <p
              class="text-white/80 text-sm sm:text-base max-w-md leading-relaxed"
            >
              Banho em Ouro 18k com proteção antialérgica. Acabamento impecável
              garantido por nossa infraestrutura de ponta.
            </p>
          </div>
        </div>

        <div
          class="benefit-card md:col-span-5 group relative rounded-[2.5rem] bg-[#F4C2C2] p-8 sm:p-10 flex flex-col justify-between min-h-[380px] sm:min-h-[450px] shadow-2xl shadow-[#F4C2C2]/10 border border-white/20 transition-all duration-500 hover:-translate-y-1"
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
            <p class="text-white/90 text-sm sm:text-base leading-relaxed">
              Receba as semijoias e só pague o que vender. Modelo de risco zero
              para você faturar desde o primeiro dia.
            </p>
          </div>
        </div>

        <div
          class="benefit-card md:col-span-4 group relative rounded-[2.5rem] bg-white border border-gray-100 overflow-hidden min-h-[350px] shadow-sm transition-all duration-500 hover:-translate-y-1"
        >
          <img
            src="../assets/Prata.png"
            alt="Coleção Prata 925"
            class="absolute inset-0 w-full h-full object-cover opacity-90 transition-all duration-700 group-hover:scale-110"
          />

          <div
            class="absolute inset-0 bg-gradient-to-t from-black/40 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"
          ></div>

          <div
            class="absolute bottom-8 left-8 transform transition-transform duration-500 group-hover:translate-x-2"
          >
            <span
              class="bg-white text-gray-950 text-[10px] px-4 py-2 rounded-full uppercase tracking-[0.2em] font-bold shadow-lg border border-gray-100"
            >
              Coleção Prata 925
            </span>
          </div>
        </div>

        <div
          class="benefit-card md:col-span-4 group relative rounded-[2.5rem] bg-[#1A1A1A] overflow-hidden min-h-[350px] shadow-xl transition-all duration-500 hover:-translate-y-1"
        >
          <img
            src="../assets/pr.jpeg"
            alt="Galvânica Própria Luby"
            class="absolute inset-0 w-full h-full object-cover opacity-40 group-hover:opacity-60 transition-opacity"
          />
          <div
            class="absolute inset-0 bg-gradient-to-t from-black via-black/20 to-transparent"
          ></div>
          <div class="relative z-10 p-8 h-full flex flex-col justify-end">
            <h3
              class="text-white text-xl sm:text-2xl font-brielle text-luby-gold mb-2 italic"
            >
              Galvânica Própria
            </h3>
            <p class="text-gray-300 text-xs sm:text-sm leading-relaxed">
              Produção interna que garante assistência imediata e banhos de alta
              resistência.
            </p>
          </div>
        </div>

        <div
          class="benefit-card md:col-span-4 group relative rounded-[2.5rem] bg-[#F4C2C2] p-8 flex flex-col justify-between min-h-[350px] shadow-2xl transition-all duration-500 hover:-translate-y-1"
        >
          <div
            class="w-12 h-12 rounded-full bg-luby-gold/10 border border-luby-gold/20 flex items-center justify-center text-luby-gold"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.2"
            >
              <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z" />
            </svg>
          </div>
          <div class="text-black">
            <h3
              class="text-xl sm:text-2xl font-brielle mb-2 text-luby-gold leading-tight"
            >
              Agilidade & Lançamentos
            </h3>
            <p class="text-gray-900 text-xs sm:text-sm leading-relaxed">
              Novidades toda semana para sua vitrine nunca parar de brilhar.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.font-brielle {
  letter-spacing: -0.01em;
}
.benefit-card {
  will-change: transform, opacity;
}
</style>
