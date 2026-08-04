<script setup lang="ts">
import { ref, watch } from 'vue';
import MagneticButton from './MagneticButton.vue';

const props = defineProps({
  show: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['update:show', 'close']);

const isOpen = ref(false);
const isSubmitted = ref(false);
const guestName = ref('');
const guestCount = ref('1');
const attending = ref('yes');
const dietaryNotes = ref('');

watch(() => props.show, (newVal) => {
  isOpen.value = newVal;
});

const closeModal = () => {
  isOpen.value = false;
  emit('update:show', false);
  emit('close');
};

const openModal = () => {
  isOpen.value = true;
  emit('update:show', true);
};

const submitForm = () => {
  if (!guestName.value.trim()) return;
  
  isSubmitted.value = true;
  
  setTimeout(() => {
    closeModal();
    setTimeout(() => {
      isSubmitted.value = false;
      guestName.value = '';
      guestCount.value = '1';
      attending.value = 'yes';
      dietaryNotes.value = '';
    }, 400);
  }, 2500);
};

defineExpose({
  openModal,
  closeModal
});
</script>

<template>
  <div>
    <!-- Floating Quick RSVP Trigger (Mobile-Friendly) -->
    <MagneticButton 
      @click="openModal"
      class="fixed bottom-5 right-5 z-[55] bg-gradient-to-r from-gold-600 via-gold-500 to-gold-600 text-white rounded-full px-5 py-3.5 shadow-2xl shadow-gold-500/35 flex items-center gap-2 hover:scale-105 active:scale-95 transition-transform cinzel tracking-widest text-xs font-bold border border-gold-300/40 cursor-pointer"
      :strength="15"
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 pointer-events-none" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
      </svg>
      <span class="pointer-events-none">RSVP</span>
    </MagneticButton>

    <!-- Modal Backdrop -->
    <Transition name="modal-fade">
      <div 
        v-if="isOpen" 
        class="fixed inset-0 z-[75] flex items-center justify-center p-4 bg-slate-950/70 backdrop-blur-md"
        @click.self="closeModal"
      >
        <div class="glass-card w-full max-w-lg rounded-3xl p-6 sm:p-8 relative shadow-2xl border border-white/90 bg-white/95 max-h-[90vh] overflow-y-auto">
          
          <!-- Close Button -->
          <button 
            @click="closeModal" 
            class="absolute top-5 right-5 w-8 h-8 rounded-full bg-slate-100 hover:bg-slate-200 text-slate-500 hover:text-slate-800 flex items-center justify-center transition-colors cursor-pointer"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <!-- Form State -->
          <div v-if="!isSubmitted">
            <div class="text-center mb-6">
              <span class="text-gold-700 text-[10px] sm:text-xs uppercase tracking-widest font-bold">Please Respond</span>
              <h2 class="cinzel text-2xl sm:text-3xl text-slate-900 font-bold tracking-wide mt-1">
                Confirm Attendance
              </h2>
              <p class="text-slate-500 text-xs mt-1">
                For the Holy Baptism of Evah Eliza Roice
              </p>
            </div>
            
            <form @submit.prevent="submitForm" class="flex flex-col gap-4">
              <!-- Full Name -->
              <div>
                <label class="block text-[11px] uppercase tracking-wider text-slate-600 font-bold mb-1.5">
                  Guest Name(s) *
                </label>
                <input 
                  v-model="guestName" 
                  type="text" 
                  required
                  placeholder="e.g. Thomas & Family" 
                  class="w-full bg-slate-50 border border-slate-200 rounded-xl px-4 py-3 text-slate-800 placeholder-slate-400 focus:outline-none focus:bg-white focus:border-gold-500 focus:ring-2 focus:ring-gold-500/20 text-sm transition-all"
                />
              </div>

              <!-- Attendance Selection -->
              <div>
                <label class="block text-[11px] uppercase tracking-wider text-slate-600 font-bold mb-1.5">
                  Will You Attend?
                </label>
                <div class="grid grid-cols-2 gap-3">
                  <label class="cursor-pointer">
                    <input type="radio" v-model="attending" value="yes" class="peer sr-only" />
                    <div class="w-full text-center py-3 px-2 border-2 border-slate-200 rounded-xl text-slate-600 peer-checked:bg-gradient-to-r peer-checked:from-gold-600 peer-checked:to-gold-500 peer-checked:text-white peer-checked:border-gold-500 transition-all uppercase tracking-wider text-xs font-bold shadow-sm">
                      Joyfully Accept
                    </div>
                  </label>
                  <label class="cursor-pointer">
                    <input type="radio" v-model="attending" value="no" class="peer sr-only" />
                    <div class="w-full text-center py-3 px-2 border-2 border-slate-200 rounded-xl text-slate-600 peer-checked:bg-slate-800 peer-checked:text-white peer-checked:border-slate-800 transition-all uppercase tracking-wider text-xs font-bold shadow-sm">
                      Regretfully Decline
                    </div>
                  </label>
                </div>
              </div>

              <!-- Number of Guests -->
              <div v-if="attending === 'yes'">
                <label class="block text-[11px] uppercase tracking-wider text-slate-600 font-bold mb-1.5">
                  Number of Attendees
                </label>
                <select 
                  v-model="guestCount"
                  class="w-full bg-slate-50 border border-slate-200 rounded-xl px-4 py-3 text-slate-800 focus:outline-none focus:bg-white focus:border-gold-500 focus:ring-2 focus:ring-gold-500/20 text-sm transition-all"
                >
                  <option value="1">1 Person</option>
                  <option value="2">2 Persons</option>
                  <option value="3">3 Persons</option>
                  <option value="4">4 Persons</option>
                  <option value="5+">5+ Persons (Family)</option>
                </select>
              </div>

              <!-- Optional Notes -->
              <div>
                <label class="block text-[11px] uppercase tracking-wider text-slate-600 font-bold mb-1.5">
                  Wishes or Dietary Notes (Optional)
                </label>
                <textarea 
                  v-model="dietaryNotes"
                  rows="2"
                  placeholder="Any blessings or special dietary requirements..." 
                  class="w-full bg-slate-50 border border-slate-200 rounded-xl px-4 py-2.5 text-slate-800 placeholder-slate-400 focus:outline-none focus:bg-white focus:border-gold-500 focus:ring-2 focus:ring-gold-500/20 text-sm transition-all resize-none"
                ></textarea>
              </div>
              
              <!-- Submit Button -->
              <button 
                type="submit" 
                class="w-full mt-2 bg-gradient-to-r from-gold-600 via-gold-500 to-gold-600 hover:from-gold-500 hover:to-gold-500 text-white rounded-xl py-3.5 uppercase tracking-widest text-xs font-bold shadow-lg shadow-gold-500/30 transition-all hover:scale-[1.01] active:scale-[0.99] cursor-pointer"
              >
                Send RSVP Confirmation
              </button>
            </form>
          </div>

          <!-- Success Confirmation -->
          <div v-else class="text-center py-8">
            <div class="w-16 h-16 bg-gold-500/20 text-gold-600 rounded-full flex items-center justify-center mx-auto mb-4 border border-gold-500/30">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7" />
              </svg>
            </div>
            <h3 class="cinzel text-2xl font-bold text-slate-900 mb-2">Thank You!</h3>
            <p class="text-slate-600 text-sm max-w-xs mx-auto">
              Your response has been warmly received. We look forward to celebrating with you!
            </p>
          </div>

        </div>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
  transform: scale(0.96);
}
</style>
