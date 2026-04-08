<script setup lang="ts">
import { onMounted, ref, onUnmounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const sectionRef = ref(null);
const bgGlow = ref(null);

const handleMouseMove = (e: MouseEvent) => {
  if (window.innerWidth < 1024) return;
  const { clientX, clientY } = e;
  // O glow agora persegue o mouse em tom Rosé suave
  gsap.to(bgGlow.value, {
    x: clientX - 250,
    y: clientY - 250,
    duration: 2,
    ease: "power3.out",
  });
};

onMounted(() => {
  // Revelação suave
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: "top bottom",
      end: "center center",
      scrub: 1.5,
    },
  });

  tl.from(".cta-container", {
    y: 100,
    opacity: 0,
    ease: "power3.out",
  });

  // Brilho passando pelas letras (Dourado sobre o Cinza Escuro)
  gsap.to(".shine-text", {
    backgroundPositionX: "200%",
    duration: 4,
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
    class="relative min-h-screen flex items-center justify-center bg-white overflow-hidden z-50 rounded-t-[5rem] -mt-20 shadow-[0_-30px_100px_rgba(244,194,194,0.2)]"
  >
    <div
      ref="bgGlow"
      class="absolute w-[300px] h-[300px] sm:w-[400px] sm:h-[400px] md:w-[500px] md:h-[500px] bg-[#F4C2C2] opacity-30 blur-[150px] pointer-events-none transition-opacity duration-1000"
    ></div>

    <div
      class="absolute inset-0 opacity-[0.03] pointer-events-none"
      style="background-image: url('https://grainy-gradients.vercel.app/noise.svg');"
    ></div>

    <div class="cta-container container mx-auto px-4 sm:px-6 relative z-10 flex flex-col items-center">
      <div class="text-center">
        <h3 class="font-mono text-luby-gold text-[10px] sm:text-xs tracking-[0.4em] sm:tracking-[0.6em] uppercase mb-8 sm:mb-10 md:mb-12 opacity-80">
          Sua Nova Fase Começa Aqui
        </h3>

        <h2 class="shine-text text-3xl sm:text-4xl md:text-5xl lg:text-[9rem] font-brielle leading-[0.9] tracking-tighter text-transparent bg-clip-text mb-8 sm:mb-12 md:mb-16 select-none">
          Semijoias na mão,<br />
          <span class="italic font-light">brilho no futuro.</span>
        </h2>

     <div class="flex flex-col items-center w-full">

          <div class="relative group cursor-pointer inline-block">
            <div class="absolute inset-0 rounded-full border border-[#F4C2C2]/50 scale-100 group-hover:scale-150 group-hover:opacity-0 transition-all duration-1000"></div>
            <div class="absolute inset-0 rounded-full border border-luby-gold/30 scale-100 group-hover:scale-[2] group-hover:opacity-0 transition-all duration-[1.5s]"></div>

            <a
              href="https://wa.me/555484249459?text=Ol%C3%A1!%20Quero%20ser%20uma%20revendedora%20Luby%20e%20fazer%20parte%20desse%20sucesso!"
              target="_blank"
              class="relative bg-[#1A1A1A] text-white w-48 h-48 sm:w-56 sm:h-56 md:w-64 md:h-64 lg:w-80 lg:h-80 rounded-full font-bold text-lg sm:text-xl md:text-2xl flex flex-col items-center justify-center transition-all duration-700 group-hover:bg-luby-gold group-hover:scale-95 shadow-2xl"
            >
              <span class="relative z-10 mb-1 sm:mb-2 uppercase tracking-tighter text-sm sm:text-base">Quero ser</span>
              <span class="relative z-10 font-brielle text-2xl sm:text-3xl md:text-4xl lg:text-5xl italic">Luby</span>

              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-6 w-6 sm:h-7 sm:w-7 md:h-8 md:w-8 mt-3 sm:mt-4 transform group-hover:translate-y-2 transition-transform"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
              </svg>
            </a>
          </div>
        </div>

        <div class="mt-12 sm:mt-16 md:mt-20 lg:mt-24 flex flex-col sm:flex-row items-center justify-center gap-6 sm:gap-8 md:gap-12">
          <div class="text-left border-l border-[#F4C2C2] pl-4 sm:pl-6">
            <p class="text-gray-900 font-brielle text-xl sm:text-2xl mb-1">98%</p>
            <p class="text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-widest">Aprovação</p>
          </div>
          <div class="text-left border-l border-[#F4C2C2] pl-4 sm:pl-6">
            <p class="text-gray-900 font-brielle text-xl sm:text-2xl mb-1">R$ 3.5k+</p>
            <p class="text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-widest">Lucro Médio</p>
          </div>
          <div class="text-left border-l border-[#F4C2C2] pl-4 sm:pl-6">
            <p class="text-gray-900 font-brielle text-xl sm:text-2xl mb-1">Risco Zero</p>
            <p class="text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-widest">Consignado Luby</p>
          </div>
        </div>
      </div>
    </div>

    <div class="absolute bottom-0 left-0 w-full h-1 bg-gradient-to-r from-transparent via-[#F4C2C2] to-transparent opacity-50"></div>
  </section>
</template>

<style scoped>
.shine-text {
  /* Gradiente: Cinza Escuro -> Ouro -> Cinza Escuro */
  background-image: linear-gradient(
    90deg,
    #1a1a1a 0%,
    #1a1a1a 40%,
    #d4af37 50%,
    #1a1a1a 60%,
    #1a1a1a 100%
  );
  background-size: 200% auto;
}

.cta-container {
  will-change: transform, opacity;
}

.font-brielle {
  letter-spacing: -0.02em;
}
</style>