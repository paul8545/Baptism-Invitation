<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const heroContainerRef = ref<HTMLElement | null>(null);
const heroPinnedRef = ref<HTMLElement | null>(null);
const hologramRef = ref<HTMLElement | null>(null);

// Mouse parallax effect for futuristic 3D floating layer
const handleMouseMove = (e: MouseEvent) => {
  if (!hologramRef.value) return;
  const { innerWidth, innerHeight } = window;
  const xOffset = (e.clientX / innerWidth - 0.5) * 20; // -10px to +10px
  const yOffset = (e.clientY / innerHeight - 0.5) * 20;

  gsap.to(hologramRef.value, {
    x: xOffset,
    y: yOffset,
    rotationY: xOffset * 0.8,
    rotationX: -yOffset * 0.8,
    duration: 0.8,
    ease: 'power2.out'
  });
};

onMounted(() => {
  window.addEventListener('mousemove', handleMouseMove);

  // Orbit rotation animation for futuristic celestial rings
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

  gsap.to('.ring-middle', {
    rotation: 360,
    duration: 55,
    repeat: -1,
    ease: 'none'
  });

  // Master GSAP Scroll-Scrub Timeline
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: heroContainerRef.value,
      start: 'top top',
      end: 'bottom bottom',
      scrub: 1.2,
      pin: heroPinnedRef.value,
      anticipatePin: 1
    }
  });

  // Scroll Cue fade out
  tl.to('.scroll-cue', { opacity: 0, y: 25, duration: 0.2 }, 0);

  // HUD Step 1 Active -> Step 2
  tl.to('.hud-step-1', { opacity: 0.3, duration: 0.5 }, 0.6)
    .to('.hud-step-2', { opacity: 1, color: '#f59e0b', duration: 0.5 }, 0.8);

  // Phase 1: Dissolve Story 1 -> Crossfade to Image 2 with micro camera push -> Reveal Story 2
  tl.to('.story-1', { opacity: 0, y: -40, scale: 0.92, filter: 'blur(12px)', duration: 1 }, 0.4)
    .to('.img-2', { opacity: 1, scale: 1.05, duration: 1.6, ease: 'power1.inOut' }, 0.7)
    .fromTo('.story-2', 
      { opacity: 0, y: 50, scale: 0.94, filter: 'blur(12px)' }, 
      { opacity: 1, y: 0, scale: 1, filter: 'blur(0px)', duration: 1.4, ease: 'power2.out' }, 
      1.1
    );

  // Phase 2: Dissolve Story 2 -> Crossfade to Image 3 -> Grand 3D Kinetic Reveal of Evah Eliza Roice
  tl.to('.hud-step-2', { opacity: 0.3, duration: 0.5 }, 2.8)
    .to('.hud-step-3', { opacity: 1, color: '#f59e0b', duration: 0.5 }, 3.0)
    .to('.story-2', { opacity: 0, y: -40, scale: 0.92, filter: 'blur(12px)', duration: 1 }, 2.9)
    .to('.img-3', { opacity: 1, scale: 1.06, duration: 1.8, ease: 'power1.inOut' }, 3.2)
    .fromTo('.story-3-elements', 
      { opacity: 0, y: 40, filter: 'blur(14px)' }, 
      { opacity: 1, y: 0, filter: 'blur(0px)', duration: 1.2, ease: 'power2.out' }, 
      3.6
    )
    // 3D Staggered Letter Reveal for Child Name
    .fromTo('.char', 
      { opacity: 0, y: 50, rotateX: 75, transformOrigin: '50% 100%' }, 
      { opacity: 1, y: 0, rotateX: 0, duration: 1.2, stagger: 0.03, ease: 'back.out(1.4)' }, 
      3.8
    )
    .fromTo('.sacred-cross-pulse', 
      { scale: 0.5, opacity: 0 }, 
      { scale: 1, opacity: 1, duration: 1.2, ease: 'elastic.out(1, 0.4)' }, 
      3.7
    );

  // Hold final majestic frame
  tl.to({}, { duration: 1.5 });
});

onUnmounted(() => {
  window.removeEventListener('mousemove', handleMouseMove);
  ScrollTrigger.getAll().forEach(t => t.kill());
});
</script>

<template>
  <section 
    ref="heroContainerRef" 
    id="story" 
    class="hero-container relative w-full bg-slate-950" 
    style="height: 380vh;"
  >
    <div 
      ref="heroPinnedRef" 
      class="hero-pinned relative w-full h-screen overflow-hidden flex items-center justify-center perspective-[1200px]"
    >
      
      <!-- Full-Bleed 100% Crystal-Clear Image Layer Stack -->
      <div class="absolute inset-0 w-full h-full bg-slate-900 overflow-hidden">
        <!-- Frame 1: Evah in Chair -->
        <img
          class="img-1 absolute inset-0 w-full h-full object-cover object-center z-10 opacity-100 will-change-transform brightness-100 contrast-100"
          src="/images/hero1.jpg"
          alt="Evah Eliza Roice smiling"
        />
        <!-- Frame 2: Evah in Blue Hat -->
        <img
          class="img-2 absolute inset-0 w-full h-full object-cover object-center z-20 opacity-0 scale-100 will-change-transform brightness-100 contrast-100"
          src="/images/hero2.jpg"
          alt="Evah in blue hat"
        />
        <!-- Frame 3: Evah in Church / Holy Celebration -->
        <img
          class="img-3 absolute inset-0 w-full h-full object-cover object-center z-30 opacity-0 scale-100 will-change-transform brightness-100 contrast-100"
          src="/images/hero3.jpg"
          alt="Evah Holy Baptism celebration"
        />
      </div>

      <!-- Futuristic Celestial Holographic Orbit Rings (SVG Animation Layer) -->
      <div class="absolute inset-0 flex items-center justify-center pointer-events-none z-32 opacity-45 mix-blend-screen">
        
        <!-- Outer Dashed Orbit Ring -->
        <svg class="ring-outer absolute w-[360px] h-[360px] sm:w-[620px] sm:h-[620px]" viewBox="0 0 600 600">
          <circle cx="300" cy="300" r="280" fill="none" stroke="url(#goldGrad)" stroke-width="1" stroke-dasharray="8 14" opacity="0.6" />
          <circle cx="580" cy="300" r="4" fill="#fbbf24" filter="drop-shadow(0 0 6px #f59e0b)" />
          <circle cx="20" cy="300" r="3" fill="#fbbf24" opacity="0.8" />
          <defs>
            <linearGradient id="goldGrad" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#fbbf24" stop-opacity="0.8" />
              <stop offset="50%" stop-color="#f59e0b" stop-opacity="0.2" />
              <stop offset="100%" stop-color="#d97706" stop-opacity="0.8" />
            </linearGradient>
          </defs>
        </svg>

        <!-- Middle Sacred Ring -->
        <svg class="ring-middle absolute w-[300px] h-[300px] sm:w-[500px] sm:h-[500px]" viewBox="0 0 500 500">
          <circle cx="250" cy="250" r="235" fill="none" stroke="#fef08a" stroke-width="0.8" stroke-dasharray="4 20" opacity="0.4" />
          <circle cx="250" cy="15" r="3.5" fill="#fef08a" filter="drop-shadow(0 0 5px #fbbf24)" />
        </svg>

        <!-- Inner Celestial Ring -->
        <svg class="ring-inner absolute w-[240px] h-[240px] sm:w-[380px] sm:h-[380px]" viewBox="0 0 400 400">
          <circle cx="200" cy="200" r="185" fill="none" stroke="url(#innerGold)" stroke-width="1" stroke-dasharray="1 8" opacity="0.5" />
          <defs>
            <linearGradient id="innerGold" x1="0%" y1="100%" x2="100%" y2="0%">
              <stop offset="0%" stop-color="#fef08a" />
              <stop offset="100%" stop-color="#f59e0b" />
            </linearGradient>
          </defs>
        </svg>

      </div>

      <!-- Subtle Optical Light Beam Rays -->
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,rgba(251,191,36,0.15)_0%,transparent_60%)] z-33 pointer-events-none"></div>

      <!-- Soft Edge Vignette Only (Center Face is completely clear, sharp and bright) -->
      <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-black/40 z-35 pointer-events-none"></div>

      <!-- HUD Top & Bottom Cyber Accents -->
      <div class="absolute top-6 left-6 right-6 z-40 flex justify-between items-center text-[10px] sm:text-xs tracking-[0.25em] text-white/70 uppercase font-mono pointer-events-none select-none">
        <div class="flex items-center gap-2">
          <span class="w-1.5 h-1.5 rounded-full bg-gold-400 animate-ping"></span>
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
        class="relative z-40 w-full max-w-4xl px-4 sm:px-6 text-center text-white flex flex-col items-center justify-center select-none pointer-events-none transform-gpu"
      >
        
        <!-- Story Beat 1: Sacred Blessing -->
        <div class="story-1 flex flex-col items-center justify-center transition-all duration-500 max-w-xl mx-auto">
          
          <div class="flex items-center gap-3 mb-4">
            <span class="h-px w-10 sm:w-16 bg-gradient-to-r from-transparent via-gold-400 to-transparent"></span>
            <span class="text-gold-300 text-xs sm:text-sm font-semibold tracking-[0.35em] uppercase drop-shadow-[0_2px_10px_rgba(0,0,0,0.85)]">
              ✦ A Sacred Blessing ✦
            </span>
            <span class="h-px w-10 sm:w-16 bg-gradient-to-r from-transparent via-gold-400 to-transparent"></span>
          </div>

          <p class="font-serif italic text-2xl sm:text-3xl md:text-4xl text-white leading-relaxed drop-shadow-[0_4px_18px_rgba(0,0,0,0.95)]">
            “Every good and perfect gift is from above, coming down from the Father of lights.”
          </p>

          <span class="text-gold-300/90 text-xs sm:text-sm tracking-[0.3em] uppercase font-medium mt-4 drop-shadow-[0_2px_10px_rgba(0,0,0,0.85)]">
            — James 1:17 —
          </span>
        </div>

        <!-- Story Beat 2: Joyful Miracle -->
        <div class="story-2 absolute inset-x-4 flex flex-col items-center justify-center opacity-0 transition-all duration-500 max-w-xl mx-auto">
          
          <span class="text-gold-300 text-xs sm:text-sm font-semibold tracking-[0.35em] uppercase mb-3 drop-shadow-[0_2px_10px_rgba(0,0,0,0.85)]">
            With Joyful Hearts
          </span>
          
          <h2 class="cinzel text-3xl sm:text-5xl md:text-6xl font-bold text-white tracking-wide leading-tight drop-shadow-[0_4px_24px_rgba(0,0,0,0.95)]">
            Welcoming God's<br/>
            <span class="shimmer-text font-black">
              Precious Miracle
            </span>
          </h2>

          <div class="flex items-center gap-3 mt-4 text-slate-200/95 text-xs sm:text-sm tracking-[0.35em] uppercase font-light drop-shadow-[0_2px_10px_rgba(0,0,0,0.85)]">
            <span>Born into Grace</span>
            <span class="text-gold-400">•</span>
            <span>Endless Love</span>
          </div>
        </div>

        <!-- Story Beat 3: Grand Climax (Child's Name Floating Nobly in Space) -->
        <div class="story-3 absolute inset-x-4 flex flex-col items-center justify-center opacity-100 transition-all duration-500 max-w-3xl mx-auto">
          
          <div class="story-3-elements flex flex-col items-center justify-center opacity-0">
            <!-- Holy Cross Watermark with Futuristic Expanding Halo -->
            <div class="sacred-cross-pulse relative inline-flex items-center justify-center w-12 h-12 sm:w-14 sm:h-14 rounded-full border border-gold-300/60 bg-black/40 backdrop-blur-md text-gold-300 text-lg sm:text-xl mb-3 shadow-[0_0_25px_rgba(245,158,11,0.6)]">
              ✝
              <span class="absolute inset-0 rounded-full border border-gold-400/40 animate-ping opacity-60"></span>
            </div>

            <span class="text-gold-300 text-[11px] sm:text-xs md:text-sm font-bold tracking-[0.4em] uppercase mb-2 drop-shadow-[0_2px_10px_rgba(0,0,0,0.85)]">
              The Sacrament of Holy Baptism
            </span>
          </div>

          <!-- Staggered Kinetic 3D Character Name (Evah Eliza Roice) -->
          <h1 class="child-name cinzel text-4xl sm:text-6xl md:text-7xl lg:text-8xl font-black tracking-wider leading-none my-2 drop-shadow-[0_8px_32px_rgba(0,0,0,0.95)] flex flex-wrap justify-center overflow-hidden">
            <span class="inline-block whitespace-nowrap mr-3 sm:mr-5">
              <span class="char inline-block">E</span><span class="char inline-block">v</span><span class="char inline-block">a</span><span class="char inline-block">h</span>
            </span>
            <span class="inline-block whitespace-nowrap mr-3 sm:mr-5">
              <span class="char inline-block">E</span><span class="char inline-block">l</span><span class="char inline-block">i</span><span class="char inline-block">z</span><span class="char inline-block">a</span>
            </span>
            <span class="inline-block whitespace-nowrap">
              <span class="char inline-block">R</span><span class="char inline-block">o</span><span class="char inline-block">i</span><span class="char inline-block">c</span><span class="char inline-block">e</span>
            </span>
          </h1>

          <div class="story-3-elements flex flex-col items-center justify-center opacity-0">
            <!-- Futuristic Quantum Light Rule -->
            <div class="flex items-center justify-center gap-3 mt-3">
              <div class="w-12 sm:w-24 h-px bg-gradient-to-r from-transparent via-gold-400 to-transparent"></div>
              <div class="w-2 h-2 rotate-45 bg-gold-300 shadow-[0_0_12px_rgba(245,158,11,1)]"></div>
              <div class="w-12 sm:w-24 h-px bg-gradient-to-r from-transparent via-gold-400 to-transparent"></div>
            </div>

            <p class="text-slate-100 font-serif italic text-sm sm:text-lg mt-3.5 drop-shadow-[0_2px_12px_rgba(0,0,0,0.95)] max-w-md">
              “A daughter is a radiant ray of God's sunshine and eternal grace.”
            </p>
          </div>

        </div>

      </div>

      <!-- Futuristic Minimalist Interactive Scroll Indicator -->
      <div class="scroll-cue absolute bottom-8 z-40 flex flex-col items-center gap-2 text-white pointer-events-none">
        <span class="text-[9px] sm:text-[10px] tracking-[0.35em] uppercase font-mono font-bold text-white/80 drop-shadow-[0_2px_8px_rgba(0,0,0,0.9)] flex items-center gap-1.5">
          <span>SCROLL TO DISCOVER</span>
        </span>
        <div class="w-4 h-8 rounded-full border border-gold-400/60 flex items-start justify-center p-1 bg-black/30 backdrop-blur-xs shadow-[0_0_10px_rgba(245,158,11,0.3)]">
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
