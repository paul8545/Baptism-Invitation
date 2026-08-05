<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const heroContainerRef = ref<HTMLElement | null>(null);
const heroPinnedRef = ref<HTMLElement | null>(null);
const hologramRef = ref<HTMLElement | null>(null);

let mouseMoveHandler: ((e: MouseEvent) => void) | null = null;

onMounted(() => {
  const isMobile = window.innerWidth < 768;

  // Only attach 3D mouse parallax on desktop devices with hover support
  if (window.matchMedia('(hover: hover) and (pointer: fine)').matches && hologramRef.value) {
    mouseMoveHandler = (e: MouseEvent) => {
      if (!hologramRef.value) return;
      const { innerWidth, innerHeight } = window;
      const xOffset = (e.clientX / innerWidth - 0.5) * 16;
      const yOffset = (e.clientY / innerHeight - 0.5) * 16;

      gsap.to(hologramRef.value, {
        x: xOffset,
        y: yOffset,
        rotationY: xOffset * 0.6,
        rotationX: -yOffset * 0.6,
        duration: 0.6,
        ease: 'power1.out'
      });
    };
    window.addEventListener('mousemove', mouseMoveHandler);
  }

  // Smooth background rotation for celestial rings
  gsap.to('.ring-outer', {
    rotation: 360,
    duration: 40,
    repeat: -1,
    ease: 'none'
  });

  gsap.to('.ring-inner', {
    rotation: -360,
    duration: 28,
    repeat: -1,
    ease: 'none'
  });

  // Master GSAP Scroll-Scrub Timeline (Highly responsive scrub for mobile)
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: heroContainerRef.value,
      start: 'top top',
      end: 'bottom bottom',
      scrub: isMobile ? 0.4 : 1.0, // Instant responsive touch tracking on mobile
      pin: heroPinnedRef.value,
      anticipatePin: 1
    }
  });

  // Scroll Cue fade out
  tl.to('.scroll-cue', { opacity: 0, y: 20, duration: 0.2 }, 0);

  // HUD Step 1 Active -> Step 2
  tl.to('.hud-step-1', { opacity: 0.3, duration: 0.4 }, 0.5)
    .to('.hud-step-2', { opacity: 1, color: '#f59e0b', duration: 0.4 }, 0.7);

  // Phase 1: Fade out Story 1 -> Crossfade to Image 2 -> Reveal Story 2 (Hardware-accelerated transforms)
  tl.to('.story-1', { opacity: 0, y: -30, scale: 0.95, duration: 0.8 }, 0.4)
    .to('.img-2', { opacity: 1, scale: 1.04, duration: 1.4, ease: 'power1.inOut' }, 0.6)
    .fromTo('.story-2', 
      { opacity: 0, y: 30, scale: 0.96 }, 
      { opacity: 1, y: 0, scale: 1, duration: 1.0, ease: 'power2.out' }, 
      1.0
    );

  // Phase 2: Fade out Story 2 -> Crossfade to Image 3 -> Grand Reveal of Evah Eliza Roice
  tl.to('.hud-step-2', { opacity: 0.3, duration: 0.4 }, 2.4)
    .to('.hud-step-3', { opacity: 1, color: '#f59e0b', duration: 0.4 }, 2.6)
    .to('.story-2', { opacity: 0, y: -30, scale: 0.95, duration: 0.8 }, 2.5)
    .to('.img-3', { opacity: 1, scale: 1.04, duration: 1.4, ease: 'power1.inOut' }, 2.7)
    .fromTo('.story-3-elements', 
      { opacity: 0, y: 30 }, 
      { opacity: 1, y: 0, duration: 1.0, ease: 'power2.out' }, 
      3.0
    )
    // 3D Staggered Letter Reveal for Child Name
    .fromTo('.char', 
      { opacity: 0, y: 35, rotateX: 60, transformOrigin: '50% 100%' }, 
      { opacity: 1, y: 0, rotateX: 0, duration: 0.9, stagger: 0.025, ease: 'back.out(1.2)' }, 
      3.1
    )
    .fromTo('.sacred-cross-pulse', 
      { scale: 0.6, opacity: 0 }, 
      { scale: 1, opacity: 1, duration: 0.9, ease: 'elastic.out(1, 0.5)' }, 
      3.0
    );

  // Hold final frame
  tl.to({}, { duration: 1.0 });
});

onUnmounted(() => {
  if (mouseMoveHandler) {
    window.removeEventListener('mousemove', mouseMoveHandler);
  }
  ScrollTrigger.getAll().forEach(t => t.kill());
});
</script>

<template>
  <section 
    ref="heroContainerRef" 
    id="story" 
    class="hero-container relative w-full bg-slate-950" 
    style="height: 320vh;"
  >
    <div 
      ref="heroPinnedRef" 
      class="hero-pinned relative w-full h-screen overflow-hidden flex items-center justify-center will-change-transform"
    >
      
      <!-- Full-Bleed 100% Crystal-Clear Image Layer Stack (Eager Preload + Precise Focal Alignment) -->
      <div class="absolute inset-0 w-full h-full bg-slate-950 overflow-hidden transform-gpu">
        <!-- Frame 1: Evah in Chair (Centered) -->
        <img
          class="img-1 absolute inset-0 w-full h-full object-cover object-[50%_40%] md:object-center z-10 opacity-100 will-change-transform brightness-100 contrast-100"
          src="/images/hero1.jpg"
          alt="Evah Eliza Roice smiling"
          loading="eager"
          fetchpriority="high"
          decoding="async"
        />
        <!-- Frame 2: Evah in Blue Hat (Calibrated for Mobile Focus on Left Subject) -->
        <img
          class="img-2 absolute inset-0 w-full h-full object-cover object-[32%_45%] md:object-center z-20 opacity-0 scale-100 will-change-transform brightness-100 contrast-100"
          src="/images/hero2.jpg"
          alt="Evah in blue hat"
          loading="eager"
          fetchpriority="high"
          decoding="async"
        />
        <!-- Frame 3: Evah in Church (Calibrated for Mobile Focus on Right Subject Face) -->
        <img
          class="img-3 absolute inset-0 w-full h-full object-cover object-[68%_25%] md:object-[65%_35%] z-30 opacity-0 scale-100 will-change-transform brightness-100 contrast-100"
          src="/images/hero3.jpg"
          alt="Evah Holy Baptism celebration"
          loading="eager"
          fetchpriority="high"
          decoding="async"
        />
      </div>

      <!-- Futuristic Celestial Holographic Orbit Rings (Clean GPU Vector Layer) -->
      <div class="absolute inset-0 flex items-center justify-center pointer-events-none z-32 opacity-35">
        
        <!-- Outer Dashed Orbit Ring -->
        <svg class="ring-outer absolute w-[340px] h-[340px] sm:w-[600px] sm:h-[600px] will-change-transform" viewBox="0 0 600 600">
          <circle cx="300" cy="300" r="280" fill="none" stroke="#fbbf24" stroke-width="1" stroke-dasharray="8 14" opacity="0.6" />
          <circle cx="580" cy="300" r="3.5" fill="#fbbf24" />
          <circle cx="20" cy="300" r="2.5" fill="#fbbf24" opacity="0.8" />
        </svg>

        <!-- Inner Celestial Ring -->
        <svg class="ring-inner absolute w-[240px] h-[240px] sm:w-[380px] sm:h-[380px] will-change-transform" viewBox="0 0 400 400">
          <circle cx="200" cy="200" r="185" fill="none" stroke="#fef08a" stroke-width="0.8" stroke-dasharray="3 12" opacity="0.5" />
        </svg>

      </div>

      <!-- Soft Edge Vignette (Center Face is completely clear, sharp and bright) -->
      <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-black/40 z-35 pointer-events-none"></div>

      <!-- HUD Top Bar -->
      <div class="absolute top-5 left-5 right-5 z-40 flex justify-between items-center text-[10px] sm:text-xs tracking-[0.25em] text-white/70 uppercase font-mono pointer-events-none select-none">
        <div class="flex items-center gap-2">
          <span class="w-1.5 h-1.5 rounded-full bg-gold-400 animate-pulse"></span>
          <span>HOLY SACRAMENT // 2026</span>
        </div>
        <div class="hidden sm:flex items-center gap-4 text-white/50">
          <span class="hud-step-1 text-gold-400 font-bold">01 BLESSING</span>
          <span>/</span>
          <span class="hud-step-2">02 MIRACLE</span>
          <span>/</span>
          <span class="hud-step-3">03 SACRAMENT</span>
        </div>
      </div>

      <!-- Floating Kinetic Storytelling Layer (Parallax 3D & Hologram Typography) -->
      <div 
        ref="hologramRef" 
        class="relative z-40 w-full max-w-4xl px-4 sm:px-6 text-center text-white flex flex-col items-center justify-center select-none pointer-events-none transform-gpu min-h-[340px]"
      >
        
        <!-- Story Beat 1: Sacred Blessing -->
        <div class="story-1 flex flex-col items-center justify-center transition-all duration-300 max-w-xl mx-auto will-change-transform">
          
          <div class="flex items-center gap-3 mb-3 sm:mb-4">
            <span class="h-px w-8 sm:w-16 bg-gradient-to-r from-transparent via-gold-400 to-transparent"></span>
            <span class="text-gold-300 text-xs sm:text-sm font-semibold tracking-[0.35em] uppercase drop-shadow-[0_2px_8px_rgba(0,0,0,0.9)]">
              ✦ A Sacred Blessing ✦
            </span>
            <span class="h-px w-8 sm:w-16 bg-gradient-to-r from-transparent via-gold-400 to-transparent"></span>
          </div>

          <p class="font-serif italic text-xl sm:text-3xl md:text-4xl text-white leading-relaxed drop-shadow-[0_4px_16px_rgba(0,0,0,0.95)]">
            “Every good and perfect gift is from above, coming down from the Father of lights.”
          </p>

          <span class="text-gold-300/90 text-[11px] sm:text-sm tracking-[0.3em] uppercase font-medium mt-3 sm:mt-4 drop-shadow-[0_2px_8px_rgba(0,0,0,0.9)]">
            — James 1:17 —
          </span>
        </div>

        <!-- Story Beat 2: Joyful Miracle -->
        <div class="story-2 absolute inset-x-4 flex flex-col items-center justify-center opacity-0 transition-all duration-300 max-w-xl mx-auto will-change-transform">
          
          <span class="text-gold-300 text-xs sm:text-sm font-semibold tracking-[0.35em] uppercase mb-2 sm:mb-3 drop-shadow-[0_2px_8px_rgba(0,0,0,0.9)]">
            With Joyful Hearts
          </span>
          
          <h2 class="cinzel text-3xl sm:text-5xl md:text-6xl font-bold text-white tracking-wide leading-tight drop-shadow-[0_4px_20px_rgba(0,0,0,0.95)]">
            Welcoming God's<br/>
            <span class="shimmer-text font-black">
              Precious Miracle
            </span>
          </h2>

          <div class="flex items-center gap-3 mt-3 sm:mt-4 text-slate-200/95 text-xs sm:text-sm tracking-[0.35em] uppercase font-light drop-shadow-[0_2px_8px_rgba(0,0,0,0.9)]">
            <span>Born into Grace</span>
            <span class="text-gold-400">•</span>
            <span>Endless Love</span>
          </div>
        </div>

        <!-- Story Beat 3: Grand Climax (Child's Name Floating Nobly in Space) -->
        <div class="story-3 absolute inset-x-4 flex flex-col items-center justify-center opacity-100 transition-all duration-300 max-w-3xl mx-auto will-change-transform">
          
          <div class="story-3-elements flex flex-col items-center justify-center opacity-0 will-change-transform">
            <!-- Holy Cross Watermark with Ethereal Halo -->
            <div class="sacred-cross-pulse relative inline-flex items-center justify-center w-11 h-11 sm:w-14 sm:h-14 rounded-full border border-gold-300/60 bg-black/40 backdrop-blur-xs text-gold-300 text-base sm:text-xl mb-2 sm:mb-3 shadow-[0_0_20px_rgba(245,158,11,0.5)]">
              ✝
              <span class="absolute inset-0 rounded-full border border-gold-400/40 animate-ping opacity-50"></span>
            </div>

            <span class="text-gold-300 text-[10px] sm:text-xs md:text-sm font-bold tracking-[0.4em] uppercase mb-1.5 sm:mb-2 drop-shadow-[0_2px_8px_rgba(0,0,0,0.9)]">
              The Sacrament of Holy Baptism
            </span>
          </div>

          <!-- Staggered Kinetic 3D Character Name (Evah Eliza Roice) -->
          <h1 class="child-name cinzel text-3xl sm:text-6xl md:text-7xl lg:text-8xl font-black tracking-wider leading-none my-1.5 sm:my-2 drop-shadow-[0_6px_28px_rgba(0,0,0,0.95)] flex flex-wrap justify-center overflow-hidden">
            <span class="inline-block whitespace-nowrap mr-2.5 sm:mr-5">
              <span class="char inline-block">E</span><span class="char inline-block">v</span><span class="char inline-block">a</span><span class="char inline-block">h</span>
            </span>
            <span class="inline-block whitespace-nowrap mr-2.5 sm:mr-5">
              <span class="char inline-block">E</span><span class="char inline-block">l</span><span class="char inline-block">i</span><span class="char inline-block">z</span><span class="char inline-block">a</span>
            </span>
            <span class="inline-block whitespace-nowrap">
              <span class="char inline-block">R</span><span class="char inline-block">o</span><span class="char inline-block">i</span><span class="char inline-block">c</span><span class="char inline-block">e</span>
            </span>
          </h1>

          <div class="story-3-elements flex flex-col items-center justify-center opacity-0 will-change-transform">
            <!-- Futuristic Light Rule -->
            <div class="flex items-center justify-center gap-3 mt-2 sm:mt-3">
              <div class="w-8 sm:w-24 h-px bg-gradient-to-r from-transparent via-gold-400 to-transparent"></div>
              <div class="w-1.5 sm:w-2 h-1.5 sm:h-2 rotate-45 bg-gold-300 shadow-[0_0_8px_rgba(245,158,11,0.8)]"></div>
              <div class="w-8 sm:w-24 h-px bg-gradient-to-r from-transparent via-gold-400 to-transparent"></div>
            </div>

            <p class="text-slate-100 font-serif italic text-xs sm:text-base md:text-lg mt-2 sm:mt-3 drop-shadow-[0_2px_10px_rgba(0,0,0,0.95)] max-w-md">
              “A daughter is a radiant ray of God's sunshine and eternal grace.”
            </p>
          </div>

        </div>

      </div>

      <!-- Futuristic Minimalist Interactive Scroll Indicator -->
      <div class="scroll-cue absolute bottom-7 z-40 flex flex-col items-center gap-1.5 text-white pointer-events-none">
        <span class="text-[9px] sm:text-[10px] tracking-[0.35em] uppercase font-mono font-bold text-white/80 drop-shadow-[0_2px_6px_rgba(0,0,0,0.9)]">
          SCROLL TO DISCOVER
        </span>
        <div class="w-4 h-7 rounded-full border border-gold-400/60 flex items-start justify-center p-1 bg-black/30 backdrop-blur-xs">
          <div class="w-1 h-2 bg-gradient-to-b from-amber-200 to-amber-500 rounded-full animate-bounce"></div>
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
.cinzel {
  font-family: 'Cinzel', serif;
}

/* Metallic Gold Shimmer Gradient for Typography */
.char,
.shimmer-text {
  background: linear-gradient(
    135deg, 
    #ffffff 0%, 
    #fef08a 25%, 
    #f59e0b 50%, 
    #ffffff 75%, 
    #fbbf24 100%
  );
  background-size: 200% auto;
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: shimmerMove 6s linear infinite;
  will-change: transform, opacity;
}

@keyframes shimmerMove {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
