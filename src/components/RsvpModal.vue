<script setup lang="ts">
import { ref } from 'vue';
import MagneticButton from './MagneticButton.vue';

const isOpen = ref(false);
const isSubmitted = ref(false);
const name = ref('');
const attending = ref('yes');

const submitForm = () => {
  if (!name.value.trim()) return;
  // Here you would normally send to a backend, we'll just show the success state
  isSubmitted.value = true;
  
  setTimeout(() => {
    isOpen.value = false;
    setTimeout(() => {
      isSubmitted.value = false;
      name.value = '';
      attending.value = 'yes';
    }, 500);
  }, 3000);
};
</script>

<template>
  <div>
    <!-- Floating Button -->
    <MagneticButton 
      @click="isOpen = true"
      class="fixed bottom-6 right-6 z-[60] bg-gold-500 text-white rounded-full px-6 py-4 shadow-lg shadow-gold-500/30 flex items-center gap-2 transition-colors hover:bg-gold-600 cinzel tracking-widest text-sm"
      :strength="20"
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 pointer-events-none" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>
      <span class="pointer-events-none">RSVP</span>
    </MagneticButton>

    <!-- Modal Overlay -->
    <div 
      v-if="isOpen" 
      class="fixed inset-0 z-[70] flex items-center justify-center p-4 bg-black/60 backdrop-blur-sm transition-opacity"
      @click.self="isOpen = false"
    >
      <div class="glass-panel w-full max-w-md rounded-2xl p-8 relative shadow-2xl animate-fade-in-up bg-white/90">
        <button @click="isOpen = false" class="absolute top-4 right-4 text-slate-400 hover:text-slate-800 transition-colors">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
        </button>

        <div v-if="!isSubmitted">
          <h2 class="cinzel text-2xl text-slate-900 mb-6 text-center">RSVP</h2>
          
          <div class="flex flex-col gap-4">
            <div>
              <label class="block text-xs uppercase tracking-widest text-slate-500 mb-2">Guest Name</label>
              <input v-model="name" type="text" placeholder="Your full name" class="w-full bg-white border border-slate-200 rounded-lg px-4 py-3 text-slate-800 focus:outline-none focus:border-gold-500 focus:ring-1 focus:ring-gold-500 transition-all" />
            </div>
            
            <div>
              <label class="block text-xs uppercase tracking-widest text-slate-500 mb-2">Will you attend?</label>
              <div class="flex gap-4">
                <label class="flex-1 cursor-pointer">
                  <input type="radio" v-model="attending" value="yes" class="peer sr-only" />
                  <div class="w-full text-center py-3 border border-slate-200 rounded-lg text-slate-600 peer-checked:bg-gold-500 peer-checked:text-white peer-checked:border-gold-500 transition-colors uppercase tracking-widest text-xs font-medium">
                    Joyfully Accept
                  </div>
                </label>
                <label class="flex-1 cursor-pointer">
                  <input type="radio" v-model="attending" value="no" class="peer sr-only" />
                  <div class="w-full text-center py-3 border border-slate-200 rounded-lg text-slate-600 peer-checked:bg-slate-800 peer-checked:text-white peer-checked:border-slate-800 transition-colors uppercase tracking-widest text-xs font-medium">
                    Regretfully Decline
                  </div>
                </label>
              </div>
            </div>
            
            <button @click="submitForm" class="w-full mt-4 bg-slate-900 hover:bg-slate-800 text-white rounded-lg py-4 uppercase tracking-widest text-sm transition-colors">
              Send RSVP
            </button>
          </div>
        </div>

        <div v-else class="text-center py-8">
          <div class="w-16 h-16 bg-gold-500/10 text-gold-500 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" /></svg>
          </div>
          <h2 class="cinzel text-2xl text-slate-900 mb-2">Thank You</h2>
          <p class="text-slate-600 font-light">We have received your response.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.animate-fade-in-up {
  animation: fadeInUp 0.4s ease-out forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
</style>
