<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const targetDate = new Date('2026-09-13T10:00:00').getTime();

const days = ref(0);
const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);

let timer: number | undefined;

const updateCountdown = () => {
  const now = new Date().getTime();
  const distance = targetDate - now;

  if (distance < 0) {
    if (timer) clearInterval(timer);
    return;
  }

  days.value = Math.floor(distance / (1000 * 60 * 60 * 24));
  hours.value = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  minutes.value = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  seconds.value = Math.floor((distance % (1000 * 60)) / 1000);
};

onMounted(() => {
  updateCountdown();
  timer = setInterval(updateCountdown, 1000) as unknown as number;
});

onUnmounted(() => {
  if (timer) clearInterval(timer);
});
</script>

<template>
  <section id="countdown" class="py-16 sm:py-24 px-4 sm:px-6 relative w-full flex flex-col items-center z-10">
    <div class="max-w-3xl w-full mx-auto text-center">
      
      <!-- Section Tag & Title -->
      <div class="mb-10 sm:mb-12 gsap-fade-up">
        <span class="inline-block px-3.5 py-1 rounded-full text-[11px] sm:text-xs font-semibold tracking-widest uppercase text-gold-700 bg-gold-500/10 border border-gold-500/20 mb-3">
          Until the Blessed Hour
        </span>
        <h2 class="cinzel text-2xl sm:text-4xl text-slate-900 font-bold tracking-wide">
          The Sacred <span class="text-gold-gradient font-extrabold">Countdown</span>
        </h2>
        <p class="text-slate-500 text-xs sm:text-sm font-light mt-2 max-w-md mx-auto">
          Counting down every blessed moment until we gather in joy and faith.
        </p>
      </div>
      
      <!-- HUD Countdown Cards Grid -->
      <div class="grid grid-cols-4 gap-2.5 sm:gap-6 max-w-xl mx-auto gsap-fade-up">
        
        <!-- Days -->
        <div class="flex flex-col items-center justify-center p-3 sm:p-5 rounded-2xl glass-card relative overflow-hidden group hover:border-gold-500/40 transition-all duration-300">
          <div class="absolute -top-6 -right-6 w-12 h-12 bg-gold-400/15 rounded-full blur-lg group-hover:bg-gold-400/30 transition-all"></div>
          <span class="cinzel text-2xl sm:text-4xl md:text-5xl font-bold text-slate-900 tracking-tight">
            {{ days.toString().padStart(2, '0') }}
          </span>
          <span class="text-[9px] sm:text-[11px] uppercase tracking-widest text-gold-600 font-bold mt-1.5 sm:mt-2">
            Days
          </span>
        </div>
        
        <!-- Hours -->
        <div class="flex flex-col items-center justify-center p-3 sm:p-5 rounded-2xl glass-card relative overflow-hidden group hover:border-gold-500/40 transition-all duration-300">
          <div class="absolute -top-6 -right-6 w-12 h-12 bg-gold-400/15 rounded-full blur-lg group-hover:bg-gold-400/30 transition-all"></div>
          <span class="cinzel text-2xl sm:text-4xl md:text-5xl font-bold text-slate-900 tracking-tight">
            {{ hours.toString().padStart(2, '0') }}
          </span>
          <span class="text-[9px] sm:text-[11px] uppercase tracking-widest text-gold-600 font-bold mt-1.5 sm:mt-2">
            Hours
          </span>
        </div>
        
        <!-- Minutes -->
        <div class="flex flex-col items-center justify-center p-3 sm:p-5 rounded-2xl glass-card relative overflow-hidden group hover:border-gold-500/40 transition-all duration-300">
          <div class="absolute -top-6 -right-6 w-12 h-12 bg-gold-400/15 rounded-full blur-lg group-hover:bg-gold-400/30 transition-all"></div>
          <span class="cinzel text-2xl sm:text-4xl md:text-5xl font-bold text-slate-900 tracking-tight">
            {{ minutes.toString().padStart(2, '0') }}
          </span>
          <span class="text-[9px] sm:text-[11px] uppercase tracking-widest text-gold-600 font-bold mt-1.5 sm:mt-2">
            Mins
          </span>
        </div>
        
        <!-- Seconds -->
        <div class="flex flex-col items-center justify-center p-3 sm:p-5 rounded-2xl glass-card relative overflow-hidden group hover:border-gold-500/40 transition-all duration-300">
          <div class="absolute -top-6 -right-6 w-12 h-12 bg-gold-400/15 rounded-full blur-lg group-hover:bg-gold-400/30 transition-all"></div>
          <span class="cinzel text-2xl sm:text-4xl md:text-5xl font-bold text-gold-600 tracking-tight">
            {{ seconds.toString().padStart(2, '0') }}
          </span>
          <span class="text-[9px] sm:text-[11px] uppercase tracking-widest text-gold-600 font-bold mt-1.5 sm:mt-2">
            Secs
          </span>
        </div>

      </div>

    </div>
  </section>
</template>
