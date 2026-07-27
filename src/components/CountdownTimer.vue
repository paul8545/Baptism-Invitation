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
  <section class="py-16 px-6 relative w-full flex flex-col items-center z-10 bg-slate-50">
    <div class="text-center mb-10 gsap-fade-up">
      <h2 class="cinzel text-2xl md:text-3xl text-gold-600 mb-2">The Countdown Begins</h2>
      <div class="w-12 h-[1px] bg-gold-500/50 mx-auto"></div>
    </div>
    
    <div class="flex flex-wrap justify-center gap-3 md:gap-8 gsap-fade-up">
      <div class="flex flex-col items-center glass-panel w-20 h-24 md:w-28 md:h-32 justify-center rounded-xl shadow-md border border-black/5 hover:-translate-y-1 transition-transform duration-300">
        <span class="cinzel text-3xl md:text-5xl text-slate-900">{{ days.toString().padStart(2, '0') }}</span>
        <span class="text-[9px] md:text-xs uppercase tracking-[0.2em] text-gold-600 font-semibold mt-2">Days</span>
      </div>
      
      <div class="flex flex-col items-center glass-panel w-20 h-24 md:w-28 md:h-32 justify-center rounded-xl shadow-md border border-black/5 hover:-translate-y-1 transition-transform duration-300">
        <span class="cinzel text-3xl md:text-5xl text-slate-900">{{ hours.toString().padStart(2, '0') }}</span>
        <span class="text-[9px] md:text-xs uppercase tracking-[0.2em] text-gold-600 font-semibold mt-2">Hours</span>
      </div>
      
      <div class="flex flex-col items-center glass-panel w-20 h-24 md:w-28 md:h-32 justify-center rounded-xl shadow-md border border-black/5 hover:-translate-y-1 transition-transform duration-300">
        <span class="cinzel text-3xl md:text-5xl text-slate-900">{{ minutes.toString().padStart(2, '0') }}</span>
        <span class="text-[9px] md:text-xs uppercase tracking-[0.2em] text-gold-600 font-semibold mt-2">Mins</span>
      </div>
      
      <div class="flex flex-col items-center glass-panel w-20 h-24 md:w-28 md:h-32 justify-center rounded-xl shadow-md border border-black/5 hover:-translate-y-1 transition-transform duration-300">
        <span class="cinzel text-3xl md:text-5xl text-slate-900">{{ seconds.toString().padStart(2, '0') }}</span>
        <span class="text-[9px] md:text-xs uppercase tracking-[0.2em] text-gold-600 font-semibold mt-2">Secs</span>
      </div>
    </div>
  </section>
</template>
