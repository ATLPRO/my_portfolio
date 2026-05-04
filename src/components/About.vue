<template>
  <section id="about" class="pt-32 pb-16 bg-gray-100 dark:bg-slate-900 transition-colors duration-300">
    <div class="container mx-auto px-6">
      <div class="flex flex-col md:flex-row items-center justify-between gap-12">
        
        <!-- Texte à gauche (Centré sur mobile) -->
        <div class="flex-1 text-center md:text-center order-2 md:order-1">
          <h1 class="font-ubuntu text-[24px] text-gray-800 dark:text-white">
            Hello! i’m <span class="font-bold">Léa AGUEDE</span>
          </h1>
          
          <h2 class="font-ubuntu font-bold text-[20px] mt-2 text-gray-700 dark:text-emerald-400">
            Full-Stack Developer
          </h2>
          
          <p class="font-ubuntu font-medium text-[16px] mt-6 leading-relaxed max-w-xl mx-auto md:mx-0 text-gray-600 dark:text-gray-300">
            Passionate about creating web and mobile experiences where technical excellence 
            meets sleek design. Welcome to my digital space.
          </p>
          
          <div class="mt-10">
            <a 
              href="#contact" 
              class="inline-block bg-emerald-800 hover:bg-emerald-700 text-white font-ubuntu font-bold py-3 px-10 rounded transition-all duration-300 shadow-lg"
            >
              Contact Me
            </a>
          </div>
        </div>

        <!-- Image à droite (Disparaît sur mobile) -->
        <div class="hidden md:flex flex-1 justify-center order-1 md:order-2">
            <div class="relative group">
              <!-- Bordure verte fine identique à ton image -->
              <!-- <div class="w-64 h-64 lg:w-72 lg:h-72 rounded-full border-2 border-emerald-600 flex items-center justify-center overflow-hidden bg-white"> -->
                <img 
                  src="@/assets/images/pp.png" 
                  alt="Léa AGUEDE" 
                  class="w-100 h-full object-cover scale-110"
                />
              <!-- </div> -->
            </div>
          </div>

      </div>
    </div>
  </section>
</template>

<script setup>
// Pas de logique complexe ici pour le moment
</script>

<style scoped>
.font-ubuntu {
  font-family: var(--font-ubuntu);
}
</style>