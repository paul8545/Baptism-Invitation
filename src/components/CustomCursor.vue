<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import { gsap } from 'gsap';

const cursorDot = ref<HTMLElement | null>(null);
const cursorOutline = ref<HTMLElement | null>(null);

const onMouseMove = (e: MouseEvent) => {
  const { clientX, clientY } = e;
  
  if (cursorDot.value && cursorOutline.value) {
    gsap.to(cursorDot.value, { x: clientX, y: clientY, duration: 0 });
    gsap.to(cursorOutline.value, { x: clientX, y: clientY, duration: 0.15, ease: 'power2.out' });
  }
};

const onMouseOver = (e: MouseEvent) => {
  const target = e.target as HTMLElement;
  if (cursorOutline.value) {
    if (target.closest('a, button, input, label, select, textarea, .glass-panel, .glass-card')) {
      gsap.to(cursorOutline.value, { 
        scale: 1.5, 
        backgroundColor: 'rgba(212,175,55,0.12)', 
        borderColor: 'rgba(212,175,55,0.9)',
        duration: 0.2 
      });
    } else {
      gsap.to(cursorOutline.value, { 
        scale: 1, 
        backgroundColor: 'transparent', 
        borderColor: 'rgba(212,175,55,0.4)',
        duration: 0.2 
      });
    }
  }
};

onMounted(() => {
  if (window.matchMedia('(hover: hover) and (pointer: fine)').matches) {
    window.addEventListener('mousemove', onMouseMove);
    window.addEventListener('mouseover', onMouseOver);
    
    const style = document.createElement('style');
    style.id = 'hide-cursor';
    style.innerHTML = `@media (hover: hover) and (pointer: fine) { * { cursor: none !important; } }`;
    document.head.appendChild(style);
  }
});

onUnmounted(() => {
  window.removeEventListener('mousemove', onMouseMove);
  window.removeEventListener('mouseover', onMouseOver);
  const style = document.getElementById('hide-cursor');
  if (style) style.remove();
});
</script>

<template>
  <div class="hidden md:block pointer-events-none fixed inset-0 z-[100] overflow-hidden">
    <div ref="cursorDot" class="absolute top-0 left-0 w-2 h-2 bg-gold-600 rounded-full -translate-x-1/2 -translate-y-1/2 shadow-[0_0_10px_rgba(212,175,55,0.8)] will-change-transform"></div>
    <div ref="cursorOutline" class="absolute top-0 left-0 w-8 h-8 border border-gold-500/40 rounded-full -translate-x-1/2 -translate-y-1/2 will-change-transform"></div>
  </div>
</template>
