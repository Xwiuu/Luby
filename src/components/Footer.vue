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
    class="footer-section bg-[#020202] pt-24 pb-12 overflow-hidden relative"
  >
    <div
      class="absolute bottom-0 left-1/2 -translate-x-1/2 w-full h-64 bg-luby-gold/5 blur-[120px] pointer-events-none"
    ></div>

    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="footer-content flex flex-col items-center text-center mb-24">
        <h3
          class="text-white font-brielle text-3xl md:text-4xl mb-8 opacity-90"
        >
          Pronta para sua
          <span class="text-luby-gold italic font-light">nova fase?</span>
        </h3>

        <button
          class="group relative overflow-hidden bg-white text-gray-950 px-10 py-4 rounded-full font-bold tracking-tight transition-all duration-500 hover:pr-14 hover:bg-luby-gold"
        >
          <span class="relative z-10 uppercase">Começar agora</span>
          <span
            class="absolute right-6 top-1/2 -translate-y-1/2 opacity-0 group-hover:opacity-100 transition-all duration-300"
          >
            →
          </span>
        </button>
      </div>

      <div class="w-full h-px bg-white/5 mb-12"></div>

      <div
        class="footer-content flex flex-col md:flex-row items-center justify-between gap-8"
      >
        <div class="flex flex-col items-center md:items-start">
          <div class="font-brielle text-2xl text-white mb-2 tracking-widest">
            LUBY<span class="text-luby-gold">.</span>
          </div>
          <p
            class="text-gray-500 font-mono text-[10px] uppercase tracking-[0.2em]"
          >
            Brilho que Transforma • 2026
          </p>
        </div>

        <nav
          class="flex gap-8 text-gray-400 font-mono text-[10px] uppercase tracking-widest"
        >
          <a href="#" class="hover:text-white transition-colors">Termos</a>
          <a href="#" class="hover:text-white transition-colors">Privacidade</a>
          <a href="#" class="hover:text-white transition-colors">Contato</a>
        </nav>

        <div class="group cursor-default">
          <p
            class="text-gray-500 font-mono text-[10px] uppercase tracking-[0.3em] flex items-center gap-2"
          >
            MADE BY
            <span
              class="text-white group-hover:text-luby-gold transition-colors duration-500 font-bold tracking-[0.5em] ml-1"
            >
              WILLIAM REIS
            </span>
          </p>
        </div>
      </div>

      <div class="mt-12 text-center">
        <p
          class="text-gray-600 font-mono text-[9px] uppercase tracking-widest opacity-40"
        >
          Luby Semijoias © Todos os direitos reservados.
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.font-brielle {
  letter-spacing: 0.05em;
}

@keyframes synx-glow {
  0% {
    text-shadow: 0 0 5px rgba(212, 175, 55, 0);
  }
  50% {
    text-shadow: 0 0 10px rgba(212, 175, 55, 0.4);
  }
  100% {
    text-shadow: 0 0 5px rgba(212, 175, 55, 0);
  }
}

.group:hover span {
  animation: synx-glow 2s infinite;
}
</style>
