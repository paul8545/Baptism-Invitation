<script setup lang="ts">
import { ref } from 'vue';

const particles = ref(
  Array.from({ length: 20 }).map((_, i) => ({
    id: i,
    size: Math.random() * 3 + 1.5, // 1.5px to 4.5px
    left: Math.random() * 100, // 0 to 100%
    duration: Math.random() * 18 + 14, // 14s to 32s
    delay: Math.random() * -25, // Negative delay to start immediately
    opacity: Math.random() * 0.35 + 0.1,
  }))
);
</script>

<template>
  <div class="fixed inset-0 pointer-events-none z-30 overflow-hidden hidden md:block">
    <div 
      v-for="p in particles" 
      :key="p.id"
      class="absolute rounded-full bg-gold-400 animate-float transform-gpu"
      :style="{
        width: `${p.size}px`,
        height: `${p.size}px`,
        left: `${p.left}%`,
        opacity: p.opacity,
        animationDuration: `${p.duration}s`,
        animationDelay: `${p.delay}s`
      }"
    ></div>
  </div>
</template>

<style scoped>
@keyframes float {
  0% {
    transform: translate3d(0, 110vh, 0);
    opacity: 0;
  }
  15% {
    opacity: 0.4;
  }
  85% {
    opacity: 0.4;
  }
  100% {
    transform: translate3d(20px, -10vh, 0);
    opacity: 0;
  }
}

.animate-float {
  animation: float linear infinite;
  will-change: transform;
}
</style>
