<script setup lang="ts">
import { ref, watch } from 'vue';
import { gsap } from 'gsap';
import { useMouseInElement } from '@vueuse/core';

const props = defineProps({
  class: {
    type: String,
    default: ''
  },
  strength: {
    type: Number,
    default: 20
  }
});

const buttonRef = ref<HTMLElement | null>(null);
const { elementX, elementY, isOutside, elementWidth, elementHeight } = useMouseInElement(buttonRef);

watch([elementX, elementY, isOutside], () => {
  if (!buttonRef.value) return;
  
  if (isOutside.value) {
    gsap.to(buttonRef.value, {
      x: 0,
      y: 0,
      duration: 0.7,
      ease: 'elastic.out(1, 0.3)'
    });
  } else {
    // Calculate distance from center
    const x = ((elementX.value - (elementWidth.value / 2)) / (elementWidth.value / 2)) * props.strength;
    const y = ((elementY.value - (elementHeight.value / 2)) / (elementHeight.value / 2)) * props.strength;

    gsap.to(buttonRef.value, {
      x,
      y,
      duration: 0.2,
      ease: 'power2.out'
    });
  }
});
</script>

<template>
  <button 
    ref="buttonRef"
    :class="props.class"
  >
    <slot />
  </button>
</template>
