<script setup lang="ts">
import { onMounted } from 'vue';
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

onMounted(() => {
  // Global fade up animations
  const elements = gsap.utils.toArray('.gsap-fade-up') as HTMLElement[];
  elements.forEach((el) => {
    gsap.fromTo(el, 
      { y: 50, opacity: 0 }, 
      { 
        y: 0, 
        opacity: 1, 
        duration: 1.5, 
        ease: 'power3.out',
        scrollTrigger: {
          trigger: el,
          start: 'top 85%',
          toggleActions: 'play none none reverse'
        }
      }
    );
  });
});
</script>

<template>
  <main class="min-h-screen bg-slate-50 w-full overflow-hidden relative">
    <CustomCursor />
    <AmbientOrbs />
    <ParticlesEffect />
    <HeroSection />
    <FamilySection />
    <CountdownTimer />
    <EventDetails />
    <OfficiantsSection />
    <RsvpModal />
  </main>
</template>

<style>
/* Add any global smooth scrolling if needed */
html {
  scroll-behavior: smooth;
}
</style>
