<script setup lang="ts">
import { ref, computed } from 'vue';
import { useMouseInElement } from '@vueuse/core';

const target = ref<HTMLElement | null>(null);
const { elementX, elementY, isOutside, elementHeight, elementWidth } = useMouseInElement(target);

const cardTransform = computed(() => {
  if (isOutside.value || elementHeight.value === 0 || elementWidth.value === 0) {
    return 'perspective(1000px) rotateX(0deg) rotateY(0deg) scale3d(1, 1, 1)';
  }
  
  const MAX_ROTATION = 10;
  
  const rX = (
    MAX_ROTATION / 2 -
    (elementY.value / elementHeight.value) * MAX_ROTATION
  ).toFixed(2);
  
  const rY = (
    (elementX.value / elementWidth.value) * MAX_ROTATION -
    MAX_ROTATION / 2
  ).toFixed(2);

  return `perspective(1000px) rotateX(${rX}deg) rotateY(${rY}deg) scale3d(1.02, 1.02, 1.02)`;
});

const glareStyle = computed(() => {
  if (isOutside.value || elementHeight.value === 0 || elementWidth.value === 0) {
    return { opacity: '0' };
  }
  const x = (elementX.value / elementWidth.value) * 100;
  const y = (elementY.value / elementHeight.value) * 100;
  return {
    opacity: '0.6',
    background: `radial-gradient(circle 220px at ${x}% ${y}%, rgba(255,255,255,0.7), transparent 80%)`,
  };
});
</script>

<template>
  <div
    ref="target"
    class="relative transition-transform duration-200 ease-out will-change-transform rounded-2xl cursor-pointer"
    :style="{ transform: cardTransform }"
  >
    <slot />
    <!-- Dynamic Specular Glare Sheen -->
    <div
      class="pointer-events-none absolute inset-0 rounded-2xl transition-opacity duration-300 z-30"
      :style="glareStyle"
    ></div>
  </div>
</template>
