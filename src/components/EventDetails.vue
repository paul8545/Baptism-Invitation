<script setup lang="ts">
import MagneticButton from './MagneticButton.vue';

const googleCalendarUrl = "https://calendar.google.com/calendar/render?action=TEMPLATE&text=Evah's+Holy+Baptism&dates=20260913T090000Z/20260913T120000Z&details=Ceremony+at+St.+Mary's+Jacobite+Syrian+Orthodox+Church,+followed+by+Reception+at+Elite+Events+and+Caterers.&location=St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+Ireland";

const handleAddToCalendar = () => {
  window.open(googleCalendarUrl, '_blank');
};

const handleCall = () => {
  window.location.href = "tel:+353000000000"; // Replace with real number
};
</script>

<template>
  <section class="py-24 px-6 relative w-full flex flex-col items-center z-10 bg-slate-100">
    <!-- Cinematic particles or subtle texture could go here -->
    
    <div class="text-center mb-16 gsap-fade-up">
      <h2 class="cinzel text-3xl md:text-5xl text-gold mb-2">The Ceremony</h2>
      <div class="w-12 h-[1px] bg-gold-500/50 mx-auto"></div>
    </div>

    <div class="w-full max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-12 text-center md:text-left">
      <!-- Ceremony Details -->
      <div class="glass-panel p-8 rounded-2xl relative overflow-hidden gsap-fade-up flex flex-col items-center md:items-start">
        <div class="absolute top-0 right-0 w-32 h-32 bg-gold-500/5 rounded-full blur-[50px]"></div>
        
        <p class="text-gold uppercase tracking-widest text-xs mb-2">Ceremony</p>
        <h3 class="cinzel text-2xl text-slate-900 mb-4">St. Mary's Jacobite Syrian<br/>Orthodox Church</h3>
        <p class="text-slate-600 font-light mb-6">Waterford, Ireland</p>
        
        <div class="w-full h-[1px] bg-black/10 mb-6"></div>
        
        <div class="flex items-center gap-4 text-slate-800">
          <div class="w-10 h-10 rounded-full border border-gold-500/30 flex items-center justify-center text-gold">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" /></svg>
          </div>
          <div class="text-left">
            <p class="font-medium text-lg">Sunday, 13 September</p>
            <p class="text-gold-600 font-light">10:00 AM</p>
          </div>
        </div>
        
        <div class="w-full h-48 mt-8 rounded-xl overflow-hidden border border-gold-500/20 opacity-80 hover:opacity-100 transition-opacity duration-500">
          <iframe 
            src="https://www.google.com/maps?q=St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+Ireland&output=embed" 
            width="100%" 
            height="100%" 
            style="border:0;" 
            allowfullscreen="true" 
            loading="lazy">
          </iframe>
        </div>
        
        <div class="w-full mt-4">
          <a href="https://www.google.com/maps/dir/?api=1&destination=St.+Mary's+Jacobite+Syrian+Orthodox+Church,+Waterford,+Ireland" target="_blank" class="w-full flex items-center justify-center gap-2 py-3 border border-gold-500/30 rounded-lg text-gold-600 hover:bg-gold-500/10 hover:border-gold-500 transition-colors duration-300 uppercase tracking-widest text-xs font-medium">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.243-4.243a8 8 0 1111.314 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
            Get Route
          </a>
        </div>
      </div>

      <!-- Reception Details -->
      <div class="glass-panel p-8 rounded-2xl relative overflow-hidden gsap-fade-up flex flex-col items-center md:items-start">
        <div class="absolute top-0 right-0 w-32 h-32 bg-gold-500/5 rounded-full blur-[50px]"></div>
        
        <p class="text-gold uppercase tracking-widest text-xs mb-2">Feast & Reception</p>
        <h3 class="cinzel text-2xl text-slate-900 mb-4">Elite Events and Caterers</h3>
        <p class="text-slate-600 font-light mb-1">Rathkieran, Carrigeen,</p>
        <p class="text-slate-600 font-light mb-6">Co. Kilkenny, X91 HK7P</p>
        
        <div class="w-full h-[1px] bg-black/10 mb-6 mt-auto"></div>
        
        <div class="flex items-center gap-4 text-slate-800">
           <div class="w-10 h-10 rounded-full border border-gold-500/30 flex items-center justify-center text-gold">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2v10z" /></svg>
          </div>
          <div class="text-left">
             <p class="font-medium">Following the Ceremony</p>
          </div>
        </div>

        <div class="w-full h-48 mt-8 rounded-xl overflow-hidden border border-gold-500/20 opacity-80 hover:opacity-100 transition-opacity duration-500">
          <iframe 
            src="https://www.google.com/maps?q=Elite+Events+and+Caterers,+Rathkieran,+Carrigeen,+Co.+Kilkenny,+X91+HK7P&output=embed" 
            width="100%" 
            height="100%" 
            style="border:0;" 
            allowfullscreen="true" 
            loading="lazy">
          </iframe>
        </div>
        
        <div class="w-full mt-4">
          <a href="https://www.google.com/maps/dir/?api=1&destination=Elite+Events+and+Caterers,+Rathkieran,+Carrigeen,+Co.+Kilkenny,+X91+HK7P" target="_blank" class="w-full flex items-center justify-center gap-2 py-3 border border-gold-500/30 rounded-lg text-gold-600 hover:bg-gold-500/10 hover:border-gold-500 transition-colors duration-300 uppercase tracking-widest text-xs font-medium">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.243-4.243a8 8 0 1111.314 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
            Get Route
          </a>
        </div>
      </div>
    </div>

    <div class="mt-16 flex flex-col sm:flex-row gap-6 justify-center w-full max-w-lg mx-auto gsap-fade-up">
      <MagneticButton @click="handleAddToCalendar" class="flex-1 group relative px-6 py-4 bg-transparent overflow-hidden rounded-full border border-gold-500/50 hover:border-gold-500 transition-colors duration-500" :strength="15">
        <div class="absolute inset-0 bg-gold-500/10 translate-y-[100%] group-hover:translate-y-0 transition-transform duration-500 ease-in-out pointer-events-none"></div>
        <span class="relative z-10 flex items-center justify-center gap-2 text-gold-600 group-hover:text-gold-500 uppercase tracking-widest text-xs font-medium transition-colors duration-300 pointer-events-none whitespace-nowrap">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" /></svg>
          Add to Calendar
        </span>
      </MagneticButton>

      <MagneticButton @click="handleCall" class="flex-1 group relative px-6 py-4 bg-gold-500 overflow-hidden rounded-full hover:bg-gold-600 transition-colors duration-500" :strength="15">
        <span class="relative z-10 flex items-center justify-center gap-2 text-white uppercase tracking-widest text-xs font-medium transition-colors duration-300 pointer-events-none whitespace-nowrap">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" /></svg>
          Call Host
        </span>
      </MagneticButton>
    </div>
  </section>
</template>
