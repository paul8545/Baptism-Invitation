<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '.hero-container',
      start: 'top top',
      end: 'bottom bottom',
      scrub: 1.5,
      pin: '.hero-pinned',
    }
  });

  // Hide scroll indicator early
  tl.to('.scroll-indicator', { opacity: 0, duration: 0.2 }, 0);

  // Phase 1: Fade out text 1, crossfade to img 2, fade in text 2
  tl.to('.text-1', { opacity: 0, y: -30, duration: 1 }, 0.5)
    .to('.img-2', { opacity: 1, duration: 1.5 }, 1)
    .to('.text-2', { opacity: 1, y: 0, duration: 1 }, 1.5);

  // Phase 2: Fade out text 2, crossfade to img 3, fade in final text 3
  tl.to('.text-2', { opacity: 0, y: -30, duration: 1 }, 3.5)
    .to('.img-3', { opacity: 1, duration: 1.5 }, 4)
    .to('.text-3', { opacity: 1, scale: 1, duration: 1.5 }, 4.5);

  // Slight zoom on the final image for cinematic effect
  tl.to('.img-3', { scale: 1.05, duration: 2 }, 4.5);

  // Phase 3: Hold the final frame for a moment before moving to the next section
  tl.to({}, { duration: 1.5 });
});

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(t => t.kill());
});
</script>

<template>
  <div class="hero-container relative w-full bg-slate-50" style="height: 400vh;">
    <div class="hero-pinned relative w-full h-screen overflow-hidden flex items-center justify-center">
      
      <!-- Background Image Sequence -->
      <div class="absolute inset-0 w-full h-full bg-white">
        <img class="img-1 absolute inset-0 w-full h-full object-cover z-10 opacity-70" src="/images/hero1.jpg" alt="Evah 1" />
        <img class="img-2 absolute inset-0 w-full h-full object-cover z-20 opacity-0" src="/images/hero2.jpg" alt="Evah 2" />
        <img class="img-3 absolute inset-0 w-full h-full object-cover z-30 opacity-0" src="/images/hero3.jpg" alt="Evah 3" />
      </div>

      <!-- Vignette Overlay to make text readable -->
      <div class="absolute inset-0 bg-gradient-to-b from-white/70 via-white/40 to-white/90 z-40"></div>

      <!-- Story Text Sequence -->
      <div class="relative z-50 w-full max-w-4xl px-6 text-center text-slate-900 h-64">
        <div class="text-1 absolute inset-0 flex items-center justify-center opacity-100 transform translate-y-0">
          <h2 class="cinzel text-3xl md:text-5xl text-gold glow-gold tracking-widest leading-relaxed">Every perfect gift<br/>is from above...</h2>
        </div>
        
        <div class="text-2 absolute inset-0 flex items-center justify-center opacity-0 transform translate-y-10">
          <h2 class="cinzel text-3xl md:text-5xl text-gold glow-gold tracking-widest leading-relaxed">A new journey<br/>of faith begins...</h2>
        </div>
        
        <div class="text-3 absolute inset-0 flex flex-col items-center justify-center opacity-0 transform scale-90">
          <p class="text-gold uppercase tracking-[0.3em] text-sm md:text-base mb-4 drop-shadow-sm">Holy Baptism Of</p>
          <h1 class="cinzel text-5xl md:text-7xl lg:text-9xl text-slate-900 glow-gold mb-2 font-medium">Evah Eliza Roice</h1>
        </div>
      </div>

      <!-- Scroll Indicator -->
      <div class="scroll-indicator absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 z-50 opacity-80 animate-bounce">
        <span class="text-[10px] uppercase tracking-[0.2em] text-gold-400">Scroll to Begin</span>
        <div class="w-[1px] h-12 bg-gradient-to-b from-gold-500 to-transparent"></div>
      </div>

    </div>
  </div>
</template>
