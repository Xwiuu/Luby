<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import { gsap } from "gsap";

// Refs para os elementos que vamos animar
const sectionRef = ref(null);
const mainVisual = ref(null);
const subtext = ref(null);
const cta = ref(null);
// Array para os objetos flutuantes (as joias)
const productItems = ref<any[]>([]);

// Função helper para adicionar múltiplos refs no array
const addToRefs = (el: any) => {
  if (el && !productItems.value.includes(el)) {
    productItems.value.push(el);
  }
};

onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: "power4.out", duration: 1.5 } });

  // 1. ANIMAÇÃO DE ENTRADA (HMR)
  tl.from(
    ".line-internal",
    { y: "100%", skewY: 7, opacity: 0, stagger: 0.1 },
    0.2,
  )
    .from(subtext.value, { y: 20, opacity: 0, duration: 1 }, 1)
    .from(cta.value, { scale: 0.8, opacity: 0, duration: 1 }, 1.2)
    .from(mainVisual.value, { x: 50, opacity: 0, duration: 2 }, 0.5);

  // 2. EFEITO PARALLAX NO MOUSE
  const mouseMoveHandler = (e: MouseEvent) => {
    if (!sectionRef.value || window.innerWidth < 1024) return; // Desativa parallax no mobile para performance

    const { clientX, clientY } = e;
    const centerX = window.innerWidth / 2;
    const centerY = window.innerHeight / 2;

    const deltaX = clientX - centerX;
    const deltaY = clientY - centerY;

    productItems.value.forEach((item, index) => {
      const factor = (index + 1) * 20;
      gsap.to(item, {
        x: deltaX / factor,
        y: deltaY / factor,
        duration: 0.5,
        ease: "power1.out",
      });
    });
  };

  window.addEventListener("mousemove", mouseMoveHandler);

  onUnmounted(() => {
    window.removeEventListener("mousemove", mouseMoveHandler);
  });
});
</script>

<template>
  <section
    ref="sectionRef"
    class="relative min-h-screen flex items-center justify-center pt-32 lg:pt-24 overflow-hidden bg-luby-nude text-gray-950"
  >
    <div class="absolute inset-0 z-0">
      <div
        class="absolute -top-20 -right-20 lg:-top-40 lg:-right-40 w-64 h-64 lg:w-96 lg:h-96 rounded-full bg-luby-gold opacity-10 blur-3xl"
      ></div>
      <div
        class="absolute bottom-20 -left-10 lg:-left-20 w-64 h-64 lg:w-80 lg:h-80 rounded-full bg-luby-rose opacity-20 blur-2xl"
      ></div>
    </div>

    <div
      class="container relative z-10 max-w-7xl mx-auto px-6 grid grid-cols-12 gap-4 lg:gap-8"
    >
      <div
        class="col-span-12 lg:col-span-7 flex flex-col justify-center text-center lg:text-left"
      >

        <h1
          ref="titleRef"
          class="font-brielle text-5xl md:text-8xl leading-[1.1] md:leading-none mb-8 md:mb-10 lg:-ml-1 flex flex-col items-center lg:items-start"
        >
          <span class="line-parent overflow-hidden block">
            <span class="line-internal block transform will-change-transform"
              >Toda mulher merece</span
            >
          </span>
          <span class="line-parent overflow-hidden block">
            <span
              class="line-internal block text-luby-gold transform will-change-transform font-light italic ml-0 lg:ml-40"
              >brilhar...</span
            >
          </span>
        </h1>

        <p
          ref="subtext"
          class="text-lg md:text-2xl font-sans text-gray-700 leading-relaxed mb-10 md:mb-12 max-w-xl mx-auto lg:mx-0"
        >
          Transforme sofisticação em
          <strong class="text-luby-gold font-semibold"
            >renda extraordinária</strong
          >. Torne-se uma revendedora exclusiva Luby e conquiste sua liberdade
          com estilo.
        </p>

        <button ref="cta" class="btn-primary bg-luby-gold text-gray-950 px-10 py-4 rounded-full font-bold text-lg hover:bg-luby-gold/90 transition-all duration-300 shadow-lg hover:shadow-xl">Começar agora</button>
      </div>

      <div
        ref="mainVisual"
        class="col-span-12 lg:col-span-5 relative flex items-center justify-center mt-16 lg:mt-0"
      >
        <div
          class="relative w-full max-w-70 md:max-w-md aspect-4/5 rounded-3xl overflow-hidden shadow-2xl border-2 border-white/40"
        >
          <img
            src="https://images.unsplash.com/photo-1596462502278-27bfdc4033c8?q=80&w=1000&auto=format&fit=crop"
            alt="High Impact Portrait"
            class="w-full h-full object-cover"
          />
        </div>

        <div
          :ref="addToRefs"
          class="absolute -right-10 -top-10 lg:-right-20 lg:-top-10 w-32 h-32 lg:w-48 lg:h-48 rounded-full border border-gray-100 bg-white/20 p-4 backdrop-blur-sm shadow-xl hidden md:flex items-center justify-center text-[10px] text-gray-400"
        >
          [PNG Joia 1]
        </div>

        <div
          :ref="addToRefs"
          class="absolute -left-8 bottom-10 lg:-left-16 lg:bottom-16 w-24 h-24 lg:w-36 lg:h-36 rounded-full border border-gray-100 bg-white/20 p-3 backdrop-blur-sm shadow-xl hidden md:flex items-center justify-center text-[10px] text-gray-400"
        >
          [PNG Joia 2]
        </div>
      </div>
    </div>

    <div
      class="absolute bottom-8 left-1/2 transform -translate-x-1/2 hidden lg:flex flex-col items-center gap-2 opacity-60"
    >
      <span class="text-xs font-mono uppercase tracking-widest text-gray-600"
        >Scroll</span
      >
      <div class="w-px h-16 bg-gray-300 relative overflow-hidden">
        <div
          class="absolute top-0 left-0 w-full h-full bg-luby-gold animate-scroll-line"
        ></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.line-internal {
  will-change: transform;
}

@keyframes scroll-line {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(100%);
  }
}
.animate-scroll-line {
  animation: scroll-line 1.5s infinite;
}
</style>
