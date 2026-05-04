<template>
  <footer class="bg-white dark:bg-slate-900 pt-12 pb-8 border-t border-gray-100 dark:border-gray-800 transition-colors duration-300">
    <div class="container mx-auto px-6">
      
      <!-- Structure en 3 colonnes sur desktop pour forcer le centrage du milieu -->
      <div class="grid grid-cols-1 md:grid-cols-3 items-center md:items-start gap-8">
        
        <!-- Gauche : Identité (Ubuntu Bold 24 / Regular 15) -->
        <div class="text-center md:text-left">
          <h2 class="font-ubuntu font-bold text-[24px] text-gray-900 dark:text-white leading-none">
            Lea AGUEDE
          </h2>
          <p class="font-ubuntu font-normal text-[15px] text-gray-600 dark:text-gray-400 mt-1">
            Full-Stack Developer
          </p>
        </div>

        <!-- Milieu : Icones & Navigation (Parfaitement centré) -->
        <div class="flex flex-col items-center gap-2">
          
          <!-- Icones Sociaux -->
          <div class="flex items-center gap-5">
            <a href="https://linkedin.com/in/Léa Aguede" target="_blank" class="transition-all hover:scale-110">
              <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" alt="LinkedIn" class="w-8 h-8" />
            </a>
            <a href="https://wa.me/237683447149" target="_blank" class="transition-all hover:scale-110">
              <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp" class="w-8 h-8" />
            </a>
            <a href="https://github.com/ATLPRO" target="_blank" class="transition-all hover:scale-110">
              <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" alt="GitHub" class="w-8 h-8 dark:invert" />
            </a>
          </div>

          <!-- Navigation Rapide (Ubuntu Bold 14) -->
          <nav class="flex flex-wrap justify-center gap-x-2 gap-y-1">
            <a v-for="link in navLinks" :key="link.name" :href="link.href" 
               class="font-ubuntu font-bold text-[12px] text-gray-900 dark:text-white hover:text-green-800 dark:hover:text-green-400 transition-colors">
              {{ link.name }}
            </a>
          </nav>
        </div>

        <!-- Droite : Vide sur desktop pour équilibrer le grid, bouton scroll à l'intérieur -->
        <div class="hidden md:block relative h-full">
           <!-- Espace réservé pour l'équilibre du centrage -->
        </div>
      </div>

      <!-- Copyright & Scroll to Top -->
      <div class="mt-6 pt-2 border-t border-gray-50 dark:border-gray-800 flex flex-col items-center relative">
        <p class="font-ubuntu font-bold text-[14px] text-gray-900 dark:text-white">
          © {{ currentYear }} @leaaguede
        </p>

        <!-- Bouton Scroll to Top (Vert sapin) -->
        <button 
          @click="scrollToTop"
          class="absolute right-0 bottom-0 p-3 bg-[#2d522d] hover:bg-[#1f3a1f] text-white rounded-full shadow-lg transition-all duration-300 hover:-translate-y-1 focus:outline-none"
          aria-label="Scroll to top"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewbox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 15l7-7 7 7" />
          </svg>
        </button>
      </div>

    </div>
  </footer>
</template>

<script setup>
import { computed } from 'vue';

// Année automatique
const currentYear = computed(() => new Date().getFullYear());

const navLinks = [
  { name: 'About me', href: '#about' },
  { name: 'My Stack', href: '#stack' },
  { name: 'Services', href: '#services' },
  { name: 'Projets', href: '#projets' },
  { name: 'Contact', href: '#contact' },
]

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
};
</script>

<style scoped>
.font-ubuntu {
  font-family: 'Ubuntu', sans-serif;
}
</style>