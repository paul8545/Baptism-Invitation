<script setup lang="ts">
import { ref, computed } from 'vue';
import { useMouseInElement } from '@vueuse/core';

const target = ref(null);
const { elementX, elementY, isOutside, elementHeight, elementWidth } = useMouseInElement(target);

const cardTransform = computed(() => {
  if (isOutside.value || elementHeight.value === 0) {
    return 'perspective(1000px) rotateX(0deg) rotateY(0deg) scale3d(1, 1, 1)';
  }
  
  const MAX_ROTATION = 12;
  
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
</script>

<template>
  <div ref="target" class="transition-transform duration-200 ease-out will-change-transform" :style="{ transform: cardTransform }">
    <slot />
  </div>
</template>
