<script setup lang="ts">
import TiltCard from './TiltCard.vue';

const familyMembers = [
  {
    name: 'Roice Varghese',
    role: 'Father',
    image: '/images/roice_father.jpg',
    badge: 'Proud Father',
    quote: 'Guiding with devotion, strength & prayer.'
  },
  {
    name: 'Jolsna',
    role: 'Mother',
    image: '/images/jolsna_mother.jpg',
    badge: 'Loving Mother',
    quote: 'Nurturing with grace, faith & gentle love.'
  },
  {
    name: 'Kunjatta',
    role: 'Sister',
    image: '/images/kunjatta_sister.jpg',
    badge: 'Adoring Sister',
    quote: 'A lifelong companion, joy & protector.'
  }
];
</script>

<template>
  <section id="family" class="py-16 sm:py-28 px-4 sm:px-6 relative w-full flex flex-col items-center z-10">
    <div class="max-w-6xl w-full mx-auto text-center">
      
      <!-- Section Header -->
      <div class="mb-12 sm:mb-16 gsap-fade-up">
        <span class="inline-block px-3.5 py-1 rounded-full text-[11px] sm:text-xs font-semibold tracking-widest uppercase text-gold-700 bg-gold-500/10 border border-gold-500/20 mb-3">
          The Blessed Household
        </span>
        <h2 class="cinzel text-2xl sm:text-4xl md:text-5xl text-slate-900 font-bold tracking-wide">
          The <span class="text-gold-gradient font-extrabold">Family</span>
        </h2>
        <p class="text-slate-600 text-xs sm:text-sm font-light mt-2.5 max-w-lg mx-auto">
          With deep gratitude to the Almighty, we invite you to share in our family's greatest joy.
        </p>
      </div>

      <!-- Family Cards Grid (Mobile-First 1-col to 3-col) -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8 justify-items-center max-w-5xl mx-auto">
        
        <TiltCard
          v-for="(member, idx) in familyMembers"
          :key="member.name"
          class="w-full max-w-xs sm:max-w-sm gsap-fade-up"
        >
          <div class="flex flex-col items-center glass-card rounded-2xl overflow-hidden shadow-xl hover:shadow-2xl hover:border-gold-500/40 transition-all duration-500 group h-full">
            
            <!-- Photo Frame with Specular Sheen -->
            <div class="w-full h-72 sm:h-80 overflow-hidden relative bg-slate-100">
              <img
                :src="member.image"
                :alt="member.name"
                class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700 ease-out"
              />
              
              <!-- Subtle vignette overlay -->
              <div class="absolute inset-0 bg-gradient-to-t from-slate-950/60 via-transparent to-transparent"></div>
              
              <!-- Role Badge -->
              <div class="absolute bottom-3 left-3 right-3 flex justify-between items-center">
                <span class="px-3 py-1 rounded-full text-[10px] sm:text-xs uppercase tracking-widest font-bold text-white bg-slate-900/80 backdrop-blur-md border border-white/20 shadow-md">
                  {{ member.badge }}
                </span>
                <span class="w-6 h-6 rounded-full bg-gold-500/80 text-white flex items-center justify-center text-xs font-bold shadow">
                  ✝
                </span>
              </div>
            </div>

            <!-- Card Info -->
            <div class="text-center w-full p-5 sm:p-6 bg-white/70 flex flex-col justify-between flex-grow">
              <div>
                <h3 class="cinzel text-lg sm:text-xl font-bold text-slate-900 tracking-wide group-hover:text-gold-700 transition-colors">
                  {{ member.name }}
                </h3>
                <p class="text-gold-600 text-xs uppercase tracking-widest font-semibold mt-1">
                  {{ member.role }}
                </p>
              </div>
              <p class="text-slate-500 text-xs italic mt-3 pt-3 border-t border-slate-100">
                “{{ member.quote }}”
              </p>
            </div>

          </div>
        </TiltCard>

      </div>

    </div>
  </section>
</template>
