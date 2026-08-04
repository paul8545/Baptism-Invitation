<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

import HeroSection from './components/HeroSection.vue';
import FamilySection from './components/FamilySection.vue';
import CountdownTimer from './components/CountdownTimer.vue';
import EventDetails from './components/EventDetails.vue';
import OfficiantsSection from './components/OfficiantsSection.vue';
import ParticlesEffect from './components/ParticlesEffect.vue';
import RsvpModal from './components/RsvpModal.vue';
import CustomCursor from './components/CustomCursor.vue';
import AmbientOrbs from './components/AmbientOrbs.vue';

gsap.registerPlugin(ScrollTrigger);

const isRsvpOpen = ref(false);

onMounted(() => {
  // Global smooth fade up animations for all sections
  const elements = gsap.utils.toArray('.gsap-fade-up') as HTMLElement[];
  elements.forEach((el) => {
    gsap.fromTo(el, 
      { y: 40, opacity: 0 }, 
      { 
        y: 0, 
        opacity: 1, 
        duration: 1.2, 
        ease: 'power2.out',
        scrollTrigger: {
          trigger: el,
          start: 'top 88%',
          toggleActions: 'play none none reverse'
        }
      }
    );
  });
});
</script>

<template>
  <div class="min-h-screen bg-[#fafaf9] text-slate-900 w-full overflow-x-hidden relative selection:bg-gold-500 selection:text-white">
    <!-- Interactive Atmosphere Effects -->
    <CustomCursor />
    <AmbientOrbs />
    <ParticlesEffect />

    <!-- Main Content Flow -->
    <main class="relative z-10 w-full">
      <HeroSection />
      <FamilySection />
      <CountdownTimer />
      <EventDetails />
      <OfficiantsSection />
    </main>

    <!-- Global RSVP Modal & Floating Trigger -->
    <RsvpModal :show="isRsvpOpen" @update:show="isRsvpOpen = $event" />

    <!-- Elegant Footer -->
    <footer class="py-12 px-6 relative z-10 border-t border-slate-200/80 bg-white/60 text-center">
      <div class="max-w-md mx-auto flex flex-col items-center">
        <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-gold-600 to-gold-400 text-white flex items-center justify-center text-xs font-bold shadow mb-3">
          ✝
        </div>
        <p class="cinzel text-sm font-bold text-slate-800 tracking-wider">
          The Holy Baptism of Evah Eliza Roice
        </p>
        <p class="text-xs text-slate-500 mt-1">
          Sunday, 13 September 2026 • Waterford & Carrigeen, Ireland
        </p>
        <p class="text-[10px] text-slate-400 uppercase tracking-widest mt-4">
          With Love & Blessings from the Family
        </p>
      </div>
    </footer>
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
}
</style>
