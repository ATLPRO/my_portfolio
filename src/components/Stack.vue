<template>
    <section id="stack" class="py-16 bg-white dark:bg-slate-900 transition-colors duration-300 overflow-hidden">
        <div class="container mx-auto px-4 md:px-6"> <!-- px-4 au lieu de 6 sur mobile -->

            <h2 v-reveal class="font-ubuntu font-bold text-[24px] text-center mb-16 text-gray-900 dark:text-white">
                My Stack
            </h2>

            <!-- gap réduit à 4 sur mobile pour gagner de la place -->
            <div class="grid grid-cols-2 md:grid-cols-6 gap-y-10 gap-x-4 md:gap-x-6 max-w-5xl mx-auto items-center justify-items-center">

                <div v-for="(tech, index) in technologies" :key="tech.name" v-reveal="{ delay: index * 100 }"
                    class="w-full max-w-[140px] md:max-w-[160px] aspect-[3/2] flex flex-col items-center justify-center bg-white dark:bg-slate-800 rounded-xl border transition-all duration-300 cursor-default stack-card group"
                    :class="{
                        'md:col-span-2': tech.name !== 'Github',
                        'md:col-start-3 md:col-span-2': tech.name === 'Github',
                        'md:col-start-1': tech.name === 'BootStrap'
                    }" 
                    :style="{
                        '--card-color': tech.color,
                        borderColor: tech.color,
                        /* Ombre réduite sur mobile pour éviter le débordement */
                        boxShadow: `0 4px 0 0 ${tech.color}44`
                    }">
                    
                    <div
                        class="mb-2 flex items-center justify-center transition-transform duration-300 group-hover:scale-110"
                        :class="tech.name === 'Figma' ? 'h-12 w-12 md:h-16 md:w-16' : 'h-10 w-10 md:h-12 md:w-12'">
                        <img :src="tech.icon" :alt="tech.name" class="max-h-full max-w-full object-contain" />
                    </div>

                    <span class="font-ubuntu font-normal text-[13px] md:text-[14px] text-gray-900 dark:text-gray-100">
                        {{ tech.name }}
                    </span>
                </div>

            </div>
        </div>
    </section>
</template>

<script setup>
// L'ordre dans ce tableau est crucial pour le placement
import vueIcon from '@/assets/images/vue.png'
import laravelIcon from '@/assets/images/laravel.png'
import tailwindIcon from '@/assets/images/tailwind.png'
import bootstrapIcon from '@/assets/images/bootstrap.png'
import nuxtIcon from '@/assets/images/nuxt.png'
import figmaIcon from '@/assets/images/figma.png'

const technologies = [
    // Ligne 1
    { name: 'Vue.js', color: '#42b883', icon: vueIcon },
    { name: 'Laravel', color: '#ff2d20', icon: laravelIcon },
    { name: 'Tailwin.css', color: '#38bdf8', icon: tailwindIcon },

    // Ligne 2 (Seul au centre)
    { name: 'Github', color: '#24292e', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg' },
    
    // Ligne 3
    { name: 'BootStrap', color: '#7952b3', icon: bootstrapIcon },
    { name: 'Nuxt.js', color: '#00dc82', icon: nuxtIcon },
    { name: 'Figma', color: '#f24e1e', icon: figmaIcon },
]

const vReveal = {
    mounted: (el, binding) => {
        el.style.opacity = "0"
        el.style.transform = "translateY(30px)"
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
.stack-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 15px -3px var(--card-color) !important;
    background-color: rgba(255, 255, 255, 0.9);
}

.font-ubuntu {
    font-family: 'Ubuntu', sans-serif;
}
</style>