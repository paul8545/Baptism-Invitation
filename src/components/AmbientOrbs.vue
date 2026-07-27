<script setup lang="ts">
import { onMounted } from 'vue';
import { gsap } from 'gsap';

onMounted(() => {
  gsap.to('.orb-1', {
    x: '20vw',
    y: '15vh',
    scale: 1.2,
    duration: 15,
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  });
  
  gsap.to('.orb-2', {
    x: '-25vw',
    y: '-20vh',
    scale: 1.1,
    duration: 22,
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  });
  
  gsap.to('.orb-3', {
    x: '15vw',
    y: '-10vh',
    scale: 1.3,
    duration: 18,
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  });
});
</script>

<template>
  <div class="fixed inset-0 pointer-events-none z-[1] overflow-hidden mix-blend-multiply opacity-50">
    <!-- Ethereal Gold Orb -->
    <div class="orb-1 absolute top-[10%] left-[10%] w-[40vw] h-[40vw] bg-gold-300 rounded-full blur-[100px] opacity-70"></div>
    
    <!-- Ethereal White Orb -->
    <div class="orb-2 absolute top-[40%] right-[5%] w-[50vw] h-[50vw] bg-white rounded-full blur-[120px] opacity-90"></div>
    
    <!-- Ethereal Deep Gold Orb -->
    <div class="orb-3 absolute bottom-[0%] left-[20%] w-[35vw] h-[35vw] bg-gold-500 rounded-full blur-[100px] opacity-60"></div>
  </div>
</template>
