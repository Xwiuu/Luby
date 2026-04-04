<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import { gsap } from "gsap";
import { ScrollToPlugin } from "gsap/ScrollToPlugin"; // Importa o plugin de scroll

gsap.registerPlugin(ScrollToPlugin);

const isScrolled = ref(false);
const isMenuOpen = ref(false);

// Mapeamento de nomes para os IDs que você criou
const menuItems = [
  { name: 'Benefícios', id: '#beneficios' },
  { name: 'Como funciona', id: '#como-funciona' },
  { name: 'Ganhos', id: '#ganhos' },
  { name: 'FAQ', id: '#faq' }
];

const handleScroll = () => {
  isScrolled.value = window.scrollY > 80;
};

// A FUNÇÃO MÁGICA DE SCROLL
const scrollToSection = (id: string) => {
  isMenuOpen.value = false; // Fecha o menu mobile se estiver aberto

  gsap.to(window, {
    duration: 1.5,
    scrollTo: {
      y: id,
      offsetY: 80 // Desconto da altura do header para não cobrir o título
    },
    ease: "power4.inOut"
  });
};

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
  if (isMenuOpen.value) {
    gsap.to(".mobile-overlay", { y: 0, opacity: 1, duration: 0.5, ease: "power4.out" });
  } else {
    gsap.to(".mobile-overlay", { y: "-100%", opacity: 0, duration: 0.4, ease: "power2.in" });
  }
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <header class="fixed top-0 left-0 w-full z-[100] flex justify-center items-center pointer-events-none">
    
    <div 
      :class="[
        'mt-4 transition-all duration-500 ease-[cubic-bezier(0.23,1,0.32,1)] pointer-events-auto flex items-center justify-between px-6 md:px-10 border border-transparent',
        isScrolled 
          ? 'w-[92%] md:w-[85%] max-w-[1100px] bg-white/70 backdrop-blur-md shadow-2xl py-3 rounded-full border-white/20' 
          : 'w-full max-w-7xl bg-transparent py-6 rounded-none'
      ]"
    >
      
      <div @click="scrollToSection('body')" class="font-brielle text-xl md:text-2xl font-bold tracking-widest text-gray-950 cursor-pointer">
        LUBY<span class="text-luby-gold">.</span>
      </div>

      <nav class="hidden md:flex items-center gap-10">
        <a v-for="item in menuItems" 
           :key="item.id" 
           href="javascript:void(0)"
           @click="scrollToSection(item.id)"
           class="text-[10px] font-mono font-bold uppercase tracking-widest text-gray-500 hover:text-gray-950 transition-colors relative group">
          {{ item.name }}
          <span class="absolute -bottom-1 left-1/2 -translate-x-1/2 w-1 h-1 bg-luby-gold rounded-full opacity-0 group-hover:opacity-100 transition-opacity"></span>
        </a>
      </nav>

      <div class="flex items-center gap-4">
        <button @click="scrollToSection('#ganhos')" class="hidden sm:block bg-gray-950 text-white px-6 py-2.5 rounded-full text-[10px] font-mono font-bold uppercase tracking-widest hover:bg-luby-gold hover:text-black transition-all">
          Seja Luby
        </button>

        <button @click="toggleMenu" class="md:hidden p-2 flex flex-col gap-1.5 items-end">
          <span :class="['h-[2px] bg-gray-950 transition-all w-6', isMenuOpen ? 'rotate-45 translate-y-2' : '']"></span>
          <span :class="['h-[2px] bg-gray-950 transition-all w-4', isMenuOpen ? 'opacity-0' : '']"></span>
          <span :class="['h-[2px] bg-gray-950 transition-all w-6', isMenuOpen ? '-rotate-45 -translate-y-2' : '']"></span>
        </button>
      </div>
    </div>

    <div class="mobile-overlay fixed inset-0 bg-white z-[120] -translate-y-full opacity-0 flex flex-col items-center justify-center gap-10 md:hidden pointer-events-auto">
      <button @click="toggleMenu" class="absolute top-10 right-10 text-4xl font-light">×</button>
      
      <a v-for="item in menuItems" 
         :key="item.id" 
         href="javascript:void(0)" 
         @click="scrollToSection(item.id)" 
         class="text-5xl font-brielle text-gray-950 hover:text-luby-gold transition-colors">
         {{ item.name }}
      </a>
      
      <button @click="scrollToSection('#ganhos')" class="mt-4 bg-gray-950 text-white px-12 py-5 rounded-full font-bold uppercase text-xs tracking-[0.2em]">
        Quero ser Luby
      </button>
    </div>

  </header>
</template>

<style scoped>
/* Evita o serrilhado no Android e melhora a renderização de fontes */
header {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Transição de curva de luxo (Apple Style) */
.transition-all {
  transition-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
}

.mobile-overlay {
  will-change: transform, opacity;
}
</style>