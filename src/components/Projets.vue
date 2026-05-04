<template>
  <section id="projets" class="py-16 bg-slate-50 dark:bg-slate-900 transition-colors duration-300 overflow-hidden">
    <div class="container mx-auto px-4 md:px-6">
      
      <!-- Titre Section -->
      <h2 v-reveal class="font-ubuntu font-bold text-[24px] text-center mb-12 text-gray-900 dark:text-white">
        Projets
      </h2>

      <!-- Grille des projets -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto">
        <div 
          v-for="(project, index) in projects" 
          :key="project.title"
          v-reveal="{ delay: index * 150 }"
          class="project-card flex flex-col bg-white dark:bg-slate-800 rounded-[15px] shadow-sm hover:shadow-xl transition-all duration-300 overflow-hidden border border-gray-100 dark:border-gray-700"
        >
          <!-- Conteneur Image -->
          <div class="relative overflow-hidden aspect-video bg-gray-200">
            <img 
              :src="project.image" 
              :alt="project.title" 
              class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
            />
          </div>

          <!-- Contenu Texte -->
          <div class="p-6 flex flex-col flex-grow justify-center items-center text-center">
            <h3 class="font-ubuntu font-bold text-[14px] text-gray-900 dark:text-white leading-tight">
              {{ project.title }}
            </h3>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// Importation des images (à adapter selon tes chemins réels)
import production from '@/assets/images/production.png'
import parck from '@/assets/images/parck.png'
import complexe from '@/assets/images/complexe.png'

const projects = [
  { 
    title: "Web application for production management", 
    image: production 
  },
  { 
    title: "Participation in the development of a web application for managing a driving school", 
    image: parck 
  },
  { 
    title: "Participation in the development of ERP systems for managing hotel complexes", 
    image: complexe 
  }
]

const vReveal = {
  mounted: (el, binding) => {
    el.style.opacity = "0"
    el.style.transform = "translateY(30px)"
    el.style.transition = `all 0.7s ease-out ${binding.value?.delay || 0}ms`
    
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          el.style.opacity = "1"
          el.style.transform = "translateY(0)"
        }
      })
    }, { threshold: 0.1 })
    observer.observe(el)
  }
}
</script>

<style scoped>
.font-ubuntu { font-family: 'Ubuntu', sans-serif; }

.project-card {
  /* Sécurité anti-débordement mobile */
  width: 100%;
  max-width: 380px;
  margin: 0 auto;
}

.project-card:hover {
  transform: translateY(-5px);
}

/* Effet de lissage pour les images */
img {
  display: block;
  max-width: 100%;
}
</style>