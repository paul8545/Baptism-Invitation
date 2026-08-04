<script setup lang="ts">
import TiltCard from './TiltCard.vue';

const bishop = {
  name: 'H.G. Thomas Mor Alexandrios',
  title: 'Metropolitan / Bishop',
  image: 'https://static.wixstatic.com/media/209604_4b1efc94c6ab4b68adc598eac6885999~mv2.jpg/v1/fill/w_800,h_1200,al_c,q_85,usm_0.66_1.00_0.01,enc_avif,quality_auto/209604_4b1efc94c6ab4b68adc598eac6885999~mv2.jpg',
  badge: 'Chief Celebrant',
};

const priests = [
  {
    name: 'Fr. Bibin Babu',
    title: 'Priest',
    image: '/images/fr_bibin_babu.jpg',
    badge: 'Co-Celebrant'
  },
  {
    name: 'Fr. Dr. Jobymon Skaria',
    title: 'Priest',
    image: '/images/priest_3.jpg',
    badge: 'Co-Celebrant'
  }
];
</script>

<template>
  <section id="clergy" class="py-16 sm:py-28 px-4 sm:px-6 relative w-full flex flex-col items-center z-10">
    <div class="max-w-6xl w-full mx-auto">
      
      <!-- Section Header -->
      <div class="text-center mb-12 sm:mb-16 gsap-fade-up">
        <span class="inline-block px-3.5 py-1 rounded-full text-[11px] sm:text-xs font-semibold tracking-widest uppercase text-gold-700 bg-gold-500/10 border border-gold-500/20 mb-3">
          Seeking Spiritual Blessings
        </span>
        <h2 class="cinzel text-2xl sm:text-4xl md:text-5xl text-slate-900 font-bold tracking-wide">
          The <span class="text-gold-gradient font-extrabold">Officiants</span>
        </h2>
        <p class="text-slate-600 text-xs sm:text-sm font-light mt-2.5 max-w-md mx-auto">
          Under the apostolic leadership and prayerful blessings of our reverend fathers.
        </p>
      </div>

      <!-- Metropolitan / Bishop Featured Spotlight Card -->
      <div class="max-w-sm sm:max-w-md mx-auto mb-10 sm:mb-14 gsap-fade-up">
        <TiltCard class="w-full">
          <div class="glass-card rounded-3xl overflow-hidden shadow-2xl border-2 border-gold-500/30 group hover:border-gold-500/60 transition-all duration-500">
            
            <div class="w-full h-80 sm:h-96 overflow-hidden relative bg-slate-900">
              <img
                :src="bishop.image"
                :alt="bishop.name"
                class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700 ease-out"
              />
              <div class="absolute inset-0 bg-gradient-to-t from-slate-950/70 via-transparent to-transparent"></div>
              
              <!-- Bishop Gold Emblem -->
              <div class="absolute top-4 right-4 w-9 h-9 rounded-full bg-gradient-to-tr from-gold-600 to-gold-400 text-white flex items-center justify-center font-bold text-sm shadow-lg border border-gold-300/50">
                ✝
              </div>

              <!-- Chief Celebrant Badge -->
              <div class="absolute bottom-4 left-4">
                <span class="px-3.5 py-1.5 rounded-full text-[10px] sm:text-xs uppercase tracking-widest font-bold text-white bg-gold-600/90 backdrop-blur-md border border-gold-300/40 shadow-lg">
                  {{ bishop.badge }}
                </span>
              </div>
            </div>

            <div class="p-6 text-center bg-white/80">
              <h3 class="cinzel text-xl sm:text-2xl font-bold text-slate-900 tracking-wide">
                {{ bishop.name }}
              </h3>
              <p class="text-gold-700 text-xs uppercase tracking-widest font-bold mt-1.5">
                {{ bishop.title }}
              </p>
            </div>

          </div>
        </TiltCard>
      </div>

      <!-- Priests Grid -->
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 sm:gap-8 max-w-2xl mx-auto">
        <TiltCard
          v-for="priest in priests"
          :key="priest.name"
          class="w-full max-w-xs mx-auto gsap-fade-up"
        >
          <div class="glass-card rounded-2xl overflow-hidden shadow-xl hover:shadow-2xl hover:border-gold-500/40 transition-all duration-500 group h-full flex flex-col justify-between">
            
            <div class="w-full h-64 sm:h-72 overflow-hidden relative bg-slate-100">
              <img
                :src="priest.image"
                :alt="priest.name"
                class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700 ease-out"
              />
              <div class="absolute inset-0 bg-gradient-to-t from-slate-950/50 via-transparent to-transparent"></div>
              
              <div class="absolute bottom-3 left-3">
                <span class="px-2.5 py-1 rounded-full text-[9px] sm:text-[10px] uppercase tracking-widest font-semibold text-white bg-slate-900/80 backdrop-blur-sm border border-white/20">
                  {{ priest.badge }}
                </span>
              </div>
            </div>

            <div class="p-5 text-center bg-white/70">
              <h4 class="cinzel text-base sm:text-lg font-bold text-slate-900 tracking-wide">
                {{ priest.name }}
              </h4>
              <p class="text-gold-600 text-xs uppercase tracking-widest font-medium mt-1">
                {{ priest.title }}
              </p>
            </div>

          </div>
        </TiltCard>
      </div>

      <!-- Sacred Blessing Quote Footer -->
      <div class="mt-20 sm:mt-28 text-center max-w-xl mx-auto gsap-fade-up">
        <div class="w-px h-12 bg-gradient-to-b from-transparent via-gold-500 to-transparent mx-auto mb-6"></div>
        <p class="cinzel text-slate-800 text-lg sm:text-2xl font-medium italic leading-relaxed">
          “I have called you by name, you are mine.”
        </p>
        <p class="text-gold-600 font-semibold text-xs sm:text-sm uppercase tracking-[0.25em] mt-2.5">
          Isaiah 43:1
        </p>
      </div>

    </div>
  </section>
</template>
