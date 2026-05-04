<script setup lang="ts">
import Header from './components/Header.vue'
import About from './components/About.vue'
import Stack from './components/Stack.vue'
import Services from './components/Services.vue'
import Projets from './components/Projets.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>
<template>
  <div class="min-h-screen bg-white dark:bg-slate-900 transition-colors duration-300">
    <Navbar />
    
    <main>
      <Header /> 
      <About />
      <Stack />
      <Services />
      <Projets />
      <Contact />
    </main>

    <Footer />
  </div>
</template>

<style scoped></style>
