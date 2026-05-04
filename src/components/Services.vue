<template>
  <!-- Ajout de overflow-hidden pour couper tout dépassement d'ombre -->
  <section id="services" class="py-16 bg-slate-100 dark:bg-slate-900 transition-colors duration-300 overflow-hidden">
    <div class="container mx-auto px-4">
      
      <h2 v-reveal class="font-ubuntu font-bold text-[24px] text-center mb-12 text-gray-900 dark:text-white">
        Services
      </h2>

      <!-- Grille avec un padding à droite (pr-2) pour laisser l'ombre respirer sans déborder -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-5xl mx-auto pr-2 pb-4">
        <div 
          v-for="(service, index) in services" 
          :key="service.title"
          v-reveal="{ delay: index * 100 }"
          class="service-card flex flex-col items-center text-center p-5 bg-white dark:bg-slate-800 rounded-[15px] border-2 transition-all duration-300 mx-auto"
          :style="{ 
            borderColor: service.color,
            boxShadow: `4px 4px 0 0 ${service.color}`,
            /* Largeur réduite sur mobile pour éviter le débordement */
            width: 'calc(100% - 10px)' 
          }"
        >
          <div class="text-3xl mb-3 h-12 w-12 flex items-center justify-center">
            <span>{{ service.emoji }}</span>
          </div>

          <h3 class="font-ubuntu font-bold text-[14px] mb-2 text-gray-900 dark:text-white uppercase tracking-wider">
            {{ service.title }}
          </h3>

          <p class="font-ubuntu font-normal text-[12px] text-gray-600 dark:text-gray-300 leading-snug">
            {{ service.description }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// Données issues de vos projets précédents (ERPs, Gestion de stock)
const services = [
  { title: "Web Development", color: "#6366f1", emoji: "💻", description: "Building responsive, fast, and scalable web applications using modern frameworks." },
  { title: "Mobile Development", color: "#d946ef", emoji: "📱", description: "Creating cross-platform mobile applications that provide a seamless user experience on both iOS and Android." },
  { title: "Backend & API Development", color: "#ef4444", emoji: "⚙️", description: "Architecting robust server-side logic and secure APIs to power your applications." },
  { title: "Management Systems (ERP/Stock)", color: "#22c55e", emoji: "📊", description: "Developing custom management tools like ERPs to solve business inventory and production issues." },
  { title: "UI/UX Design", color: "#f43f5e", emoji: "🎨", description: "Designing intuitive and aesthetically pleasing interfaces that put the user first." },
  { title: "Maintenance & Optimization", color: "#f59e0b", emoji: "🛠️", description: "Ensuring your applications stay up-to-date, secure, and optimized for the best performance." }
]

const vReveal = {
  mounted: (el, binding) => {
    el.style.opacity = "0"
    el.style.transform = "translateY(20px)"
    el.style.transition = `all 0.6s ease-out ${binding.value?.delay || 0}ms`
    
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

.service-card {
  box-sizing: border-box;
  /* On s'assure que la carte ne dépasse jamais le conteneur */
  max-width: 320px; 
}

@media (min-width: 768px) {
  .service-card {
    max-width: 100%;
  }
}

.service-card:hover {
  transform: translate(-2px, -2px);
  box-shadow: 6px 6px 0 0 var(--tw-shadow-color) !important;
}
</style>