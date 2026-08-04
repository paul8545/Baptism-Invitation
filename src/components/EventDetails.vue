<script setup lang="ts">
import MagneticButton from './MagneticButton.vue';

const googleCalendarUrl = "https://calendar.google.com/calendar/render?action=TEMPLATE&text=Evah's+Holy+Baptism&dates=20260913T090000Z/20260913T130000Z&details=The+Holy+Baptism+of+Evah+Eliza+Roice+at+St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+followed+by+Feast+at+Elite+Events+and+Caterers,+Carrigeen.&location=St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+Ireland";

const handleAddToCalendar = () => {
  window.open(googleCalendarUrl, '_blank');
};

const handleCall = () => {
  window.location.href = "tel:+353000000000";
};
</script>

<template>
  <section id="events" class="py-16 sm:py-28 px-4 sm:px-6 relative w-full flex flex-col items-center z-10">
    <div class="max-w-6xl w-full mx-auto">
      
      <!-- Section Header -->
      <div class="text-center mb-12 sm:mb-16 gsap-fade-up">
        <span class="inline-block px-3.5 py-1 rounded-full text-[11px] sm:text-xs font-semibold tracking-widest uppercase text-gold-700 bg-gold-500/10 border border-gold-500/20 mb-3">
          Order of the Sacred Day
        </span>
        <h2 class="cinzel text-2xl sm:text-4xl md:text-5xl text-slate-900 font-bold tracking-wide">
          Event <span class="text-gold-gradient font-extrabold">Schedule & Venues</span>
        </h2>
        <p class="text-slate-600 text-xs sm:text-sm font-light mt-2.5 max-w-lg mx-auto">
          We look forward to sharing these sacred moments and celebration with you.
        </p>
      </div>

      <!-- Dual Venue Cards Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 sm:gap-8 max-w-5xl mx-auto">
        
        <!-- Ceremony Card -->
        <div class="glass-card p-6 sm:p-8 rounded-3xl relative overflow-hidden flex flex-col justify-between gsap-fade-up hover:border-gold-500/40 transition-all duration-300">
          <div class="absolute -top-12 -right-12 w-32 h-32 bg-gold-400/15 rounded-full blur-2xl pointer-events-none"></div>
          
          <div>
            <!-- Badge & Icon -->
            <div class="flex items-center justify-between mb-4">
              <span class="px-3 py-1 rounded-full text-[10px] sm:text-xs uppercase tracking-widest font-bold text-gold-700 bg-gold-500/15 border border-gold-500/25">
                Sacrament Ceremony
              </span>
              <div class="w-8 h-8 rounded-full bg-gold-500/15 text-gold-600 flex items-center justify-center font-bold text-sm">
                ✝
              </div>
            </div>

            <!-- Title & Location -->
            <h3 class="cinzel text-xl sm:text-2xl font-bold text-slate-900 leading-snug">
              St. Mary's Jacobite Syrian<br/>Orthodox Church
            </h3>
            <p class="text-slate-600 text-xs sm:text-sm font-normal mt-1 mb-5 flex items-center gap-1.5">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-gold-600 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.243-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              Waterford, Ireland
            </p>

            <div class="w-full h-px bg-slate-200/80 mb-5"></div>

            <!-- Time & Date Highlight -->
            <div class="flex items-center gap-3.5 bg-gold-500/10 p-3.5 rounded-xl border border-gold-500/20">
              <div class="w-10 h-10 rounded-lg bg-gold-500 text-white flex items-center justify-center shadow-sm shrink-0">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <p class="text-xs sm:text-sm font-bold text-slate-900">Sunday, 13 September 2026</p>
                <p class="text-gold-700 text-xs font-semibold">10:00 AM Sharp</p>
              </div>
            </div>
          </div>

          <!-- Embedded Map -->
          <div class="w-full h-44 sm:h-52 mt-5 rounded-xl overflow-hidden border border-slate-200 shadow-inner">
            <iframe 
              src="https://www.google.com/maps?q=St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+Ireland&output=embed" 
              width="100%" 
              height="100%" 
              style="border:0;" 
              allowfullscreen="true" 
              loading="lazy">
            </iframe>
          </div>

          <!-- Get Route Button -->
          <a
            href="https://www.google.com/maps/dir/?api=1&destination=St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+Ireland" 
            target="_blank" 
            class="mt-4 w-full flex items-center justify-center gap-2 py-3 rounded-xl bg-slate-900 hover:bg-gold-600 text-white font-medium text-xs uppercase tracking-wider transition-colors shadow-md group cursor-pointer"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 group-hover:scale-110 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 4m0 13V4m0 0L9 7" />
            </svg>
            Get Route to Church
          </a>
        </div>

        <!-- Reception Card -->
        <div class="glass-card p-6 sm:p-8 rounded-3xl relative overflow-hidden flex flex-col justify-between gsap-fade-up hover:border-gold-500/40 transition-all duration-300">
          <div class="absolute -top-12 -right-12 w-32 h-32 bg-gold-400/15 rounded-full blur-2xl pointer-events-none"></div>
          
          <div>
            <!-- Badge & Icon -->
            <div class="flex items-center justify-between mb-4">
              <span class="px-3 py-1 rounded-full text-[10px] sm:text-xs uppercase tracking-widest font-bold text-gold-700 bg-gold-500/15 border border-gold-500/25">
                Feast & Reception
              </span>
              <div class="w-8 h-8 rounded-full bg-gold-500/15 text-gold-600 flex items-center justify-center font-bold text-sm">
                🥂
              </div>
            </div>

            <!-- Title & Location -->
            <h3 class="cinzel text-xl sm:text-2xl font-bold text-slate-900 leading-snug">
              Elite Events and Caterers
            </h3>
            <p class="text-slate-600 text-xs sm:text-sm font-normal mt-1 mb-5 flex items-center gap-1.5">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-gold-600 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.243-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              Rathkieran, Carrigeen, Co. Kilkenny, X91 HK7P
            </p>

            <div class="w-full h-px bg-slate-200/80 mb-5"></div>

            <!-- Time & Date Highlight -->
            <div class="flex items-center gap-3.5 bg-gold-500/10 p-3.5 rounded-xl border border-gold-500/20">
              <div class="w-10 h-10 rounded-lg bg-gold-500 text-white flex items-center justify-center shadow-sm shrink-0">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2v10z" />
                </svg>
              </div>
              <div>
                <p class="text-xs sm:text-sm font-bold text-slate-900">Celebration & Dining</p>
                <p class="text-gold-700 text-xs font-semibold">Immediately following the Church Ceremony</p>
              </div>
            </div>
          </div>

          <!-- Embedded Map -->
          <div class="w-full h-44 sm:h-52 mt-5 rounded-xl overflow-hidden border border-slate-200 shadow-inner">
            <iframe 
              src="https://www.google.com/maps?q=Elite+Events+and+Caterers,+Rathkieran,+Carrigeen,+Co.+Kilkenny,+X91+HK7P&output=embed" 
              width="100%" 
              height="100%" 
              style="border:0;" 
              allowfullscreen="true" 
              loading="lazy">
            </iframe>
          </div>

          <!-- Get Route Button -->
          <a
            href="https://www.google.com/maps/dir/?api=1&destination=Elite+Events+and+Caterers,+Rathkieran,+Carrigeen,+Co.+Kilkenny,+X91+HK7P" 
            target="_blank" 
            class="mt-4 w-full flex items-center justify-center gap-2 py-3 rounded-xl bg-slate-900 hover:bg-gold-600 text-white font-medium text-xs uppercase tracking-wider transition-colors shadow-md group cursor-pointer"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 group-hover:scale-110 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 4m0 13V4m0 0L9 7" />
            </svg>
            Get Route to Reception
          </a>
        </div>

      </div>

      <!-- Action Buttons Bar -->
      <div class="mt-12 sm:mt-16 flex flex-col sm:flex-row gap-4 sm:gap-6 justify-center items-center max-w-md mx-auto gsap-fade-up">
        
        <!-- Add to Calendar -->
        <MagneticButton
          @click="handleAddToCalendar"
          class="w-full sm:flex-1 py-3.5 px-6 rounded-full glass-card hover:border-gold-500 text-slate-800 font-semibold text-xs uppercase tracking-widest transition-all duration-300 shadow-md flex items-center justify-center gap-2.5 cursor-pointer"
          :strength="12"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gold-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
          </svg>
          <span>Add to Calendar</span>
        </MagneticButton>

        <!-- Call Host -->
        <MagneticButton
          @click="handleCall"
          class="w-full sm:flex-1 py-3.5 px-6 rounded-full bg-gradient-to-r from-gold-600 via-gold-500 to-gold-600 hover:from-gold-500 hover:to-gold-500 text-white font-semibold text-xs uppercase tracking-widest transition-all duration-300 shadow-lg shadow-gold-500/25 flex items-center justify-center gap-2.5 cursor-pointer"
          :strength="12"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
          </svg>
          <span>Contact / Call</span>
        </MagneticButton>

      </div>

    </div>
  </section>
</template>
