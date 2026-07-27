<script setup lang="ts">
import { ref } from 'vue';

const particles = ref(
  Array.from({ length: 40 }).map((_, i) => ({
    id: i,
    size: Math.random() * 4 + 1, // 1px to 5px
    left: Math.random() * 100, // 0 to 100%
    duration: Math.random() * 20 + 15, // 15s to 35s
    delay: Math.random() * -30, // Negative delay to start immediately
    opacity: Math.random() * 0.4 + 0.1,
  }))
);
</script>

<template>
  <div class="fixed inset-0 pointer-events-none z-50 overflow-hidden mix-blend-multiply">
    <div 
      v-for="p in particles" 
      :key="p.id"
      class="absolute rounded-full bg-gold-400 animate-float"
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
    transform: translateY(110vh) translateX(0px) scale(1);
    opacity: 0;
  }
  10% {
    opacity: var(--tw-bg-opacity, 1);
  }
  50% {
    transform: translateY(50vh) translateX(30px) scale(1.5);
  }
  90% {
    opacity: var(--tw-bg-opacity, 1);
  }
  100% {
    transform: translateY(-10vh) translateX(-30px) scale(1);
    opacity: 0;
  }
}

.animate-float {
  animation: float linear infinite;
}
</style>
