<script setup lang="ts">
import TiltCard from './TiltCard.vue';
</script>

<template>
  <section class="py-24 px-6 relative w-full flex flex-col items-center z-10">
    <div class="text-center mb-16 gsap-fade-up">
      <h2 class="cinzel text-3xl md:text-5xl text-gold mb-2">The Family</h2>
      <div class="w-12 h-[1px] bg-gold-500/50 mx-auto"></div>
    </div>

    <div class="w-full max-w-4xl mx-auto flex flex-col md:flex-row gap-12 justify-center items-center">
      <!-- Father -->
      <TiltCard class="gsap-fade-up">
        <div class="flex flex-col items-center glass-panel rounded-2xl overflow-hidden w-64 md:w-72 shadow-lg group h-full">
          <div class="w-full h-72 md:h-80 overflow-hidden relative">
            <img src="/images/roice_father.jpg" alt="Roice Varghese" class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700" />
          </div>
          <div class="text-center w-full py-6 bg-white/40">
            <h3 class="cinzel text-xl text-slate-900 tracking-wide">Roice Varghese</h3>
            <p class="text-gold-600 text-xs uppercase tracking-widest mt-2 font-medium">Father</p>
          </div>
        </div>
      </TiltCard>

      <!-- Mother -->
      <TiltCard class="gsap-fade-up">
        <div class="flex flex-col items-center glass-panel rounded-2xl overflow-hidden w-64 md:w-72 shadow-lg group h-full">
          <div class="w-full h-72 md:h-80 overflow-hidden relative">
            <img src="/images/jolsna_mother.jpg" alt="Jolsna" class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700" />
          </div>
          <div class="text-center w-full py-6 bg-white/40">
            <h3 class="cinzel text-xl text-slate-900 tracking-wide">Jolsna</h3>
            <p class="text-gold-600 text-xs uppercase tracking-widest mt-2 font-medium">Mother</p>
          </div>
        </div>
      </TiltCard>
    </div>

    <!-- Sister -->
    <TiltCard class="mt-12 gsap-fade-up">
      <div class="flex flex-col items-center glass-panel rounded-2xl overflow-hidden w-56 md:w-64 shadow-lg group">
        <div class="w-full h-64 md:h-72 overflow-hidden relative">
          <img src="/images/kunjatta_sister.jpg" alt="Kunjatta" class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700" />
        </div>
        <div class="text-center w-full py-6 bg-white/40">
          <h3 class="cinzel text-xl text-slate-900 tracking-wide">Kunjatta</h3>
          <p class="text-gold-600 text-xs uppercase tracking-widest mt-2 font-medium">Sister</p>
        </div>
      </div>
    </TiltCard>
  </section>
</template>
