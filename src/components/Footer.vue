<script setup lang="ts">
import { onMounted } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  gsap.from(".footer-content", {
    y: 20,
    opacity: 0,
    duration: 1,
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".footer-section",
      start: "top 95%",
    },
  });
});
</script>

<template>
  <footer
    class="footer-section bg-[#FFF5F2] pt-16 sm:pt-20 md:pt-24 pb-8 sm:pb-10 md:pb-12 overflow-hidden relative border-t border-[#F4C2C2]/20"
  >
    <div
      class="absolute bottom-0 left-1/2 -translate-x-1/2 w-full h-32 sm:h-48 md:h-64 bg-luby-gold/10 blur-[120px] pointer-events-none"
    ></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 relative z-10">
      
      <div class="footer-content flex flex-col items-center text-center mb-16 sm:mb-20 md:mb-24">
        <h3
          class="text-gray-900 font-brielle text-2xl sm:text-3xl md:text-5xl mb-6 sm:mb-8 leading-tight"
        >
          Pronta para sua <br>
          <span class="text-luby-gold italic font-light underline decoration-[#F4C2C2] decoration-1 underline-offset-8">nova fase de brilho?</span>
        </h3>

        <button
          class="group relative overflow-hidden bg-[#1A1A1A] text-white px-8 sm:px-10 md:px-12 py-3 sm:py-4 md:py-5 rounded-full font-bold tracking-widest transition-all duration-500 hover:bg-luby-gold hover:shadow-xl shadow-lg"
        >
          <span class="relative z-10 uppercase text-[10px] sm:text-xs">Fale com a nossa Equipe</span>
        </button>
      </div>

      <div class="w-full h-px bg-gray-200 mb-8 sm:mb-10 md:mb-12"></div>

      <div
        class="footer-content flex flex-col md:flex-row items-center justify-between gap-6 sm:gap-8"
      >
        <div class="flex flex-col items-center md:items-start">
          <div class="font-brielle text-xl sm:text-2xl text-gray-900 mb-2 tracking-widest">
            LUBY<span class="text-luby-gold">.</span>
          </div>
          <p
            class="text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-[0.2em]"
          >
            Semijoias que Transformam • 2026
          </p>
        </div>

        <nav
          class="flex gap-6 sm:gap-8 text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-widest"
        >
          <a href="#" class="hover:text-luby-gold transition-colors">Termos</a>
          <a href="#" class="hover:text-luby-gold transition-colors">Privacidade</a>
          <a href="#" class="hover:text-luby-gold transition-colors">Contato</a>
        </nav>

        <div class="group cursor-default">
          <p
            class="text-gray-400 font-mono text-[9px] sm:text-[10px] uppercase tracking-[0.3em] flex items-center gap-2"
          >
            MADE BY
            <span
              class="text-gray-900 group-hover:text-luby-gold transition-colors duration-500 font-bold tracking-[0.5em] ml-1"
            >
              WR
            </span>
          </p>
        </div>
      </div>

      <div class="mt-8 sm:mt-10 md:mt-12 text-center">
        <p
          class="text-gray-400 font-mono text-[8px] sm:text-[9px] uppercase tracking-widest opacity-60"
        >
          Luby Semijoias © Todos os direitos reservados.
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.font-brielle {
  letter-spacing: 0.02em;
}

@keyframes synx-glow {
  0% {
    text-shadow: 0 0 5px rgba(212, 175, 55, 0);
  }
  50% {
    text-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
  }
  100% {
    text-shadow: 0 0 5px rgba(212, 175, 55, 0);
  }
}

.group:hover span {
  animation: synx-glow 2s infinite;
}
</style>