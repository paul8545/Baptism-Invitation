<script setup lang="ts">
import TiltCard from './TiltCard.vue';
</script>

<template>
  <section class="py-24 px-6 relative w-full flex flex-col items-center z-10 bg-white border-t border-black/5">
    
    <div class="text-center mb-16 gsap-fade-up">
      <h2 class="cinzel text-3xl md:text-5xl text-gold mb-2">The Officiants</h2>
      <div class="w-12 h-[1px] bg-gold-500/50 mx-auto mb-4"></div>
      <p class="text-slate-500 uppercase tracking-widest text-xs font-light">Seeking Blessings</p>
    </div>

    <!-- Bishop -->
    <TiltCard class="w-full max-w-sm mx-auto mb-16 gsap-fade-up">
      <div class="flex flex-col items-center glass-panel rounded-2xl overflow-hidden shadow-lg group h-full">
        <div class="w-full h-80 overflow-hidden relative bg-black/5">
          <img src="https://static.wixstatic.com/media/209604_4b1efc94c6ab4b68adc598eac6885999~mv2.jpg/v1/fill/w_800,h_1200,al_c,q_85,usm_0.66_1.00_0.01,enc_avif,quality_auto/209604_4b1efc94c6ab4b68adc598eac6885999~mv2.jpg" alt="H.G. Thomas Mor Alexandrios" class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700" />
        </div>
        <div class="text-center w-full py-6 bg-white/40">
          <h3 class="cinzel text-xl text-slate-900 tracking-wide">H.G. Thomas Mor Alexandrios</h3>
          <p class="text-gold-600 text-xs uppercase tracking-widest mt-2 font-medium">Metropolitan / Bishop</p>
        </div>
      </div>
    </TiltCard>

    <!-- Priests -->
    <div class="w-full max-w-4xl mx-auto flex flex-col md:flex-row gap-12 justify-center items-center">
      <TiltCard class="gsap-fade-up">
        <div class="flex flex-col items-center glass-panel rounded-2xl overflow-hidden w-64 md:w-72 shadow-lg group h-full">
          <div class="w-full h-72 md:h-80 overflow-hidden relative">
            <img src="/images/fr_bibin_babu.jpg" alt="Fr. Bibin Babu" class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700" />
          </div>
          <div class="text-center w-full py-6 bg-white/40">
            <h3 class="cinzel text-lg text-slate-900 tracking-wide">Fr. Bibin Babu</h3>
            <p class="text-slate-500 text-xs uppercase tracking-widest mt-2 font-medium">Priest</p>
          </div>
        </div>
      </TiltCard>

      <TiltCard class="gsap-fade-up">
        <div class="flex flex-col items-center glass-panel rounded-2xl overflow-hidden w-64 md:w-72 shadow-lg group h-full">
          <div class="w-full h-72 md:h-80 overflow-hidden relative">
            <!-- Using priest_3.jpg as fallback for Fr. Dr. Jobymon Skaria -->
            <img src="/images/priest_3.jpg" alt="Fr. Dr. Jobymon Skaria" class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700" />
          </div>
          <div class="text-center w-full py-6 bg-white/40">
            <h3 class="cinzel text-lg text-slate-900 tracking-wide">Fr. Dr. Jobymon Skaria</h3>
            <p class="text-slate-500 text-xs uppercase tracking-widest mt-2 font-medium">Priest</p>
          </div>
        </div>
      </TiltCard>
    </div>

    <div class="mt-32 mb-12 text-center gsap-fade-up">
      <div class="w-1 h-16 bg-gradient-to-b from-transparent via-gold-500 to-transparent mx-auto mb-8 opacity-50"></div>
      <p class="cinzel text-gold text-2xl mb-4 italic">"I have called you by name, you are mine."</p>
      <p class="text-slate-400 font-light text-sm uppercase tracking-[0.3em]">Isaiah 43:1</p>
    </div>

  </section>
</template>
