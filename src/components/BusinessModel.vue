<script setup lang="ts">
import { onMounted, ref } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const sectionRef = ref(null);

const commissions = [
  {
    label: "Semente",
    percent: 20,
    desc: "Seu primeiro passo na independência.",
    range: "Até R$ 700",
  },
  {
    label: "Crescimento",
    percent: 30,
    desc: "Acelerando os lucros com segurança.",
    range: "R$ 701 a R$ 1.000",
  },
  {
    label: "Expansão",
    percent: 40,
    desc: "Construindo uma carteira sólida.",
    range: "R$ 1.001 a R$ 2.000",
  },
  {
    label: "Elite Luby",
    percent: 50,
    desc: "O topo do jogo. Metade é seu.",
    range: "Acima de R$ 2.001",
  },
];

onMounted(() => {
  // 1. EFEITO DE REVELAÇÃO DA SEÇÃO (LAYER STACKING)
  gsap.fromTo(
    sectionRef.value,
    { clipPath: "inset(15% 10% 15% 10% round 3rem)" },
    {
      clipPath: "inset(0% 0% 0% 0% round 0rem)",
      ease: "none",
      scrollTrigger: {
        trigger: sectionRef.value,
        start: "top bottom",
        end: "top top",
        scrub: true,
      },
    },
  );

  // 2. ANIMAÇÃO DOS NÚMEROS (CONTADOR E REVELAÇÃO)
  const rows = gsap.utils.toArray(".comm-item");
  rows.forEach((row: any, i) => {
    const num = row.querySelector(".num-val");
    const target = commissions[i].percent;

    gsap.context(() => {
      gsap.from(row, {
        opacity: 0,
        x: i % 2 === 0 ? -100 : 100,
        duration: 1.5,
        ease: "expo.out",
        scrollTrigger: {
          trigger: row,
          start: "top 85%",
          toggleActions: "play none none reverse",
        },
      });

      // O Contador Mágico
      gsap.to(num, {
        innerText: target,
        duration: 2,
        snap: { innerText: 1 },
        ease: "power2.out",
        scrollTrigger: {
          trigger: row,
          start: "top 85%",
        },
      });
    });
  });
});
</script>

<template>
  <section
    ref="sectionRef"
    class="relative bg-[#080808] text-white py-40 overflow-hidden z-30 shadow-[0_0_100px_rgba(0,0,0,1)]"
  >
    <div
      class="absolute top-0 left-0 w-full h-full pointer-events-none opacity-20"
    >
      <div
        class="absolute top-1/4 -left-20 w-96 h-96 bg-luby-gold rounded-full blur-[150px] animate-pulse"
      ></div>
      <div
        class="absolute bottom-1/4 -right-20 w-96 h-96 bg-luby-rose rounded-full blur-[150px] opacity-30"
      ></div>
    </div>

    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="mb-32">
        <div class="inline-flex items-center gap-4 mb-8">
          <div class="h-px w-20 bg-luby-gold"></div>
          <span
            class="text-luby-gold font-mono text-sm tracking-[0.4em] uppercase"
            >The Profit Plan</span
          >
        </div>
        <h2 class="text-6xl md:text-8xl font-brielle leading-[0.9] mb-12">
          Ganhos que <br />
          <span class="italic text-gray-500 font-light">evoluem com você.</span>
        </h2>
        <p class="max-w-xl text-gray-400 text-xl font-light leading-relaxed">
          Sem risco, sem investimento inicial e com a maior comissão do mercado
          de semijoias.
          <span class="text-white"
            >Nós bancamos o seu estoque, você comanda o lucro.</span
          >
        </p>
      </div>

      <div class="grid grid-cols-1 gap-4">
        <div
          v-for="(item, index) in commissions"
          :key="index"
          class="comm-item group relative py-12 border-b border-white/10 flex flex-col md:flex-row md:items-center justify-between transition-all duration-500 hover:border-luby-gold"
        >
          <div
            class="max-w-sm mb-6 md:mb-0 transform group-hover:translate-x-4 transition-transform duration-500"
          >
            <span
              class="text-luby-gold font-mono text-xs uppercase tracking-widest mb-2 block"
              >{{ item.label }}</span
            >
            <h4 class="text-2xl font-brielle text-white mb-2">
              {{ item.range }}
            </h4>
            <p class="text-gray-500 text-sm italic">{{ item.desc }}</p>
          </div>

          <div class="relative flex items-center justify-center md:justify-end">
            <div
              class="flex items-baseline font-brielle transition-all duration-500 group-hover:scale-110"
            >
              <span
                class="num-val text-8xl md:text-[12rem] leading-none text-transparent bg-clip-text bg-gradient-to-b from-white to-gray-700 group-hover:from-luby-gold group-hover:to-[#b8860b]"
              >
                0
              </span>
              <span class="text-4xl md:text-6xl text-luby-gold ml-2">%</span>
            </div>

            <div
              class="absolute -bottom-2 left-0 w-0 h-0.5 bg-luby-gold group-hover:w-full transition-all duration-1000"
            ></div>
          </div>
        </div>
      </div>

      <div class="mt-32 flex flex-col items-center">
        <div class="relative p-px rounded-full overflow-hidden group">
          <div
            class="absolute inset-0 bg-gradient-to-r from-transparent via-luby-gold to-transparent animate-[spin_4s_linear_infinite] opacity-0 group-hover:opacity-100 transition-opacity"
          ></div>

          <button
            class="relative bg-white text-gray-950 px-12 py-6 rounded-full font-bold text-xl flex items-center gap-4 transition-all group-hover:bg-[#050505] group-hover:text-white"
          >
            QUERO ESSA MARGEM DE 50%
            <span
              class="w-8 h-8 rounded-full bg-gray-950 text-white flex items-center justify-center group-hover:bg-luby-gold group-hover:text-gray-950"
            >
              →
            </span>
          </button>
        </div>
        <p
          class="mt-6 text-gray-500 font-mono text-xs uppercase tracking-widest"
        >
          Vagas limitadas por região
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Efeito de revelar a seção como se estivesse empilhando */
.comm-item {
  perspective: 1000px;
}

/* Tipografia com gradiente (Fallback para navegadores antigos) */
.num-val {
  -webkit-background-clip: text;
  background-clip: text;
}
</style>
