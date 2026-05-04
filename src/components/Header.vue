<template>
  <nav class="fixed w-full top-0 z-50 bg-white dark:bg-slate-900 border-b border-gray-100 dark:border-gray-800 transition-colors duration-300">
    <div class="container mx-auto px-6 py-4 flex justify-between items-center">
      
      <!-- Logo -->
      <div class="text-2xl font-bold text-emerald-800 dark:text-emerald-500 flex items-center leading-none">
        <span class="text-4xl">&lt;</span>
        <span class="-mx-0.5 mt-1">ATL</span>
        <span class="text-4xl">&gt;</span>
      </div>

      <!-- Actions (DarkMode + Burger) -->
      <div class="flex items-center space-x-4">
        <!-- Toggle Dark Mode -->
        <button @click="toggleDarkMode" class="p-2 rounded-full hover:bg-gray-100 dark:hover:bg-gray-800 transition-all duration-300">
          <svg v-if="!isDark" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-800" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364-6.364l-.707.707M6.343 17.657l-.707.707M16.071 16.071l.707.707M7.757 7.757l.707.707M12 8a4 4 0 100 8 4 4 0 000-8z" />
          </svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-yellow-400" fill="currentColor" viewBox="0 0 24 24">
            <path d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
          </svg>
        </button>

        <!-- Bouton Burger (Mobile uniquement) -->
        <button @click="isMenuOpen = !isMenuOpen" class="md:hidden p-2 text-gray-600 dark:text-gray-300">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Menu de Navigation (Desktop) -->
      <ul class="hidden md:flex items-center space-x-8 font-semibold text-gray-900 dark:text-gray-100">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" class="hover:text-emerald-700 dark:hover:text-emerald-400 transition-colors">{{ link.name }}</a>
        </li>
      </ul>
    </div>

    <!-- Menu Mobile (Liste déroulante) -->
    <transition enter-active-class="transition duration-200 ease-out" enter-from-class="transform scale-95 opacity-0" enter-to-class="transform scale-100 opacity-100" leave-active-class="transition duration-100 ease-in" leave-from-class="transform scale-100 opacity-100" leave-to-class="transform scale-95 opacity-0">
      <ul v-if="isMenuOpen" class="md:hidden bg-white dark:bg-slate-900 px-6 py-4 space-y-4 border-t border-gray-100 dark:border-gray-800 font-semibold shadow-xl">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" @click="isMenuOpen = false" class="block text-gray-900 dark:text-gray-100 hover:text-emerald-700 dark:hover:text-emerald-400">
            {{ link.name }}
          </a>
        </li>
      </ul>
    </transition>
  </nav>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const isDark = ref(false)
const isMenuOpen = ref(false)

const links = [
  { name: 'My Stack', href: '#stack' },
  { name: 'Services', href: '#services' },
  { name: 'Projets', href: '#projets' },
  { name: 'Contact', href: '#contact' }
]

const toggleDarkMode = () => {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  isDark.value = savedTheme === 'dark' || (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)
  document.documentElement.classList.toggle('dark', isDark.value)
})
</script>