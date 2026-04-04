<script setup lang="ts">
import { onMounted, ref, onUnmounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const sectionRef = ref(null);
const bgGlow = ref(null);

// 1. MOUSE TRACKING PARA O GLOW DE OURO LÍQUIDO
const handleMouseMove = (e: MouseEvent) => {
  const { clientX, clientY } = e;
  gsap.to(bgGlow.value, {
    x: clientX - 250,
    y: clientY - 250,
    duration: 2,
    ease: "power3.out",
  });
};

onMounted(() => {
  // 2. REVELAÇÃO CINEMATOGRÁFICA (ZOOM OUT EXPANSION)
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: "top bottom",
      end: "center center",
      scrub: 1.5,
    },
  });

  tl.from(".cta-container", {
    scale: 0.8,
    opacity: 0,
    filter: "blur(20px)",
    ease: "none",
  });

  // 3. ANIMAÇÃO DE TEXTO "SHINE" (O brilho passando pelas letras)
  gsap.to(".shine-text", {
    backgroundPositionX: "200%",
    duration: 3,
    repeat: -1,
    ease: "linear",
  });

  window.addEventListener("mousemove", handleMouseMove);
});

onUnmounted(() => {
  window.removeEventListener("mousemove", handleMouseMove);
});
</script>

<template>
  <section
    ref="sectionRef"
    class="relative min-h-screen flex items-center justify-center bg-[#020202] overflow-hidden z-50 rounded-t-[5rem] -mt-20"
  >
    <div
      ref="bgGlow"
      class="absolute w-125 h-125 bg-luby-gold opacity-10 blur-[150px] pointer-events-none transition-opacity duration-1000 group-hover:opacity-20"
    ></div>

    <div
      class="absolute inset-0 opacity-[0.04] pointer-events-none mix-blend-overlay"
      style="
        background-image: url(&quot;https://grainy-gradients.vercel.app/noise.svg&quot;);
      "
    ></div>

    <div
      class="cta-container container mx-auto px-6 relative z-10 flex flex-col items-center"
    >
      <div class="text-center">
        <h3
          class="font-mono text-luby-gold text-xs tracking-[0.6em] uppercase mb-12 opacity-60"
        >
          Final Chapter • Your Turn
        </h3>

        <h2
          class="shine-text text-6xl md:text-[11rem] font-brielle leading-[0.85] tracking-tighter text-transparent bg-clip-text mb-16 select-none"
        >
          Ouro nas mãos,<br />
          <span class="italic font-light">brilho na vida.</span>
        </h2>

        <div class="relative group cursor-pointer">
          <div
            class="absolute inset-0 rounded-full border border-luby-gold/30 scale-100 group-hover:scale-150 group-hover:opacity-0 transition-all duration-1000"
          ></div>
          <div
            class="absolute inset-0 rounded-full border border-luby-gold/20 scale-100 group-hover:scale-[2] group-hover:opacity-0 transition-all duration-[1.5s]"
          ></div>

          <button
            class="relative bg-white text-gray-950 w-64 h-64 md:w-80 md:h-80 rounded-full font-bold text-xl md:text-2xl flex flex-col items-center justify-center transition-transform duration-700 group-hover:scale-95 group-hover:bg-luby-gold group-hover:text-black"
          >
            <span class="relative z-10 mb-2 uppercase tracking-tighter"
              >Quero ser</span
            >
            <span class="relative z-10 font-brielle text-4xl md:text-5xl italic"
              >Luby</span
            >

            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-8 w-8 mt-4 transform group-hover:translate-y-2 transition-transform"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M19 14l-7 7m0 0l-7-7m7 7V3"
              />
            </svg>
          </button>
        </div>

        <div
          class="mt-20 flex flex-col md:flex-row items-center justify-center gap-12"
        >
          <div class="text-left border-l border-white/10 pl-6">
            <p class="text-white font-brielle text-2xl mb-1">98%</p>
            <p
              class="text-gray-500 font-mono text-[10px] uppercase tracking-widest"
            >
              Taxa de Aprovação
            </p>
          </div>
          <div class="text-left border-l border-white/10 pl-6">
            <p class="text-white font-brielle text-2xl mb-1">R$ 3.5k+</p>
            <p
              class="text-gray-500 font-mono text-[10px] uppercase tracking-widest"
            >
              Média Lucro/Mês
            </p>
          </div>
          <div class="text-left border-l border-white/10 pl-6">
            <p class="text-white font-brielle text-2xl mb-1">Consignado</p>
            <p
              class="text-gray-500 font-mono text-[10px] uppercase tracking-widest"
            >
              Risco Zero Luby
            </p>
          </div>
        </div>
      </div>
    </div>

    <div
      class="absolute bottom-0 left-0 w-full h-1 bg-gradient-to-r from-transparent via-luby-gold to-transparent opacity-30"
    ></div>
  </section>
</template>

<style scoped>
/* O Segredo do Título: Gradiente que corre infinitamente */
.shine-text {
  background-image: linear-gradient(
    90deg,
    #fff 0%,
    #fff 40%,
    #d4af37 50%,
    #fff 60%,
    #fff 100%
  );
  background-size: 200% auto;
}

/* Suavidade extrema para o scroll */
.cta-container {
  will-change: transform, filter, opacity;
}

/* Tipografia Awwwards */
.font-brielle {
  letter-spacing: -0.04em;
}
</style>
