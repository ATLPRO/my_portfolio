<template>
  <section id="contact" class="py-20 bg-slate-100 dark:bg-slate-900 transition-colors duration-300 overflow-hidden">
    <div class="container mx-auto px-4">
      
      <h2 v-reveal class="font-ubuntu font-bold text-[24px] text-center mb-12 text-gray-900 dark:text-white">
        Contact me
      </h2>

      <div 
        v-reveal="{ delay: 200 }"
        class="max-w-2xl mx-auto bg-white dark:bg-slate-800 p-8 md:p-12 rounded-[15px] shadow-xl border border-gray-100 dark:border-gray-700"
      >
        <!-- Formulaire avec VeeValidate -->
        <form @submit="onSubmit" class="space-y-6">
          
          <!-- Champ Nom -->
          <div class="relative">
            <input 
              v-model="name"
              v-bind="nameAttrs"
              type="text" 
              placeholder="Name"
              class="w-full px-4 py-3 rounded-lg border-2 bg-transparent outline-none transition-colors font-ubuntu text-[14px]"
              :class="errors.name ? 'border-red-500' : 'border-slate-200 dark:border-slate-600 focus:border-slate-400'"
            />
            <span class="text-red-500 text-xs mt-1">{{ errors.name }}</span>
          </div>

          <!-- Champ Email -->
          <div class="relative">
            <input 
              v-model="email"
              v-bind="emailAttrs"
              type="email" 
              placeholder="E-mail"
              class="w-full px-4 py-3 rounded-lg border-2 bg-transparent outline-none transition-colors font-ubuntu text-[14px]"
              :class="errors.email ? 'border-red-500' : 'border-slate-200 dark:border-slate-600 focus:border-slate-400'"
            />
            <span class="text-red-500 text-xs mt-1">{{ errors.email }}</span>
          </div>

          <!-- Champ Message -->
          <div class="relative">
            <textarea 
              v-model="message"
              v-bind="messageAttrs"
              rows="4" 
              placeholder="Message"
              class="w-full px-4 py-3 rounded-lg border-2 bg-transparent outline-none transition-colors font-ubuntu text-[14px] resize-none"
              :class="errors.message ? 'border-red-500' : 'border-slate-200 dark:border-slate-600 focus:border-slate-400'"
            ></textarea>
            <span class="text-red-500 text-xs mt-1">{{ errors.message }}</span>
          </div>

          <!-- Bouton Envoyer avec état de chargement -->
          <div class="flex justify-center pt-4">
            <button 
              type="submit" 
              :disabled="isSubmitting"
              class="px-12 py-3 bg-[#2d522d] hover:bg-[#1f3a1f] text-white font-ubuntu font-bold text-[16px] rounded-md transition-all duration-300 shadow-md hover:shadow-lg active:scale-95 disabled:opacity-50 disabled:cursor-not-allowed"
            >
              {{ isSubmitting ? 'Sending...' : 'Send' }}
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { useForm } from 'vee-validate';
import * as yup from 'yup';
import emailjs from '@emailjs/browser';
import { ref } from 'vue';

// 1. Définition du schéma de validation avec Yup
const schema = yup.object({
  name: yup.string().required('Le nom est requis').min(3, 'Minimum 3 caractères'),
  email: yup.string().email('Email invalide').required('L\'email est requis'),
  message: yup.string().required('Le message ne peut pas être vide').min(10, 'Message trop court'),
});

// 2. Initialisation de VeeValidate
const { errors, handleSubmit, defineField, resetForm, isSubmitting } = useForm({
  validationSchema: schema,
});

const [name, nameAttrs] = defineField('name');
const [email, emailAttrs] = defineField('email');
const [message, messageAttrs] = defineField('message');

// 3. Fonction d'envoi EmailJS
const onSubmit = handleSubmit(async (values) => {
  try {
    // REMPLACE CES VALEURS PAR TES IDS EMAILJS
    const SERVICE_ID = "service_j16ttcv";
    const TEMPLATE_ID = "template_ky63ked";
    const PUBLIC_KEY = "LDpeTsbc9CYjJDJx4";

    const templateParams = {
      from_name: values.name,
      from_email: values.email,
      message: values.message,
    };

    await emailjs.send(SERVICE_ID, TEMPLATE_ID, templateParams, PUBLIC_KEY);

    alert("Merci Léa, ton message a bien été envoyé !");
    resetForm();
  } catch (error) {
    console.error('Erreur EmailJS:', error);
    alert("Oups, une erreur est survenue lors de l'envoi.");
  }
});

// Directive v-reveal
const vReveal = {
  mounted: (el, binding) => {
    el.style.opacity = "0";
    el.style.transform = "translateY(20px)";
    el.style.transition = `all 0.6s ease-out ${binding.value?.delay || 0}ms`;
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          el.style.opacity = "1";
          el.style.transform = "translateY(0)";
        }
      });
    }, { threshold: 0.1 });
    observer.observe(el);
  }
};
</script>

<style scoped>
.font-ubuntu {
  font-family: 'Ubuntu', sans-serif;
}

/* Style spécifique pour les placeholders pour qu'ils ressemblent à ton image */
::placeholder {
  color: #64748b;
  opacity: 0.8;
}

/* Suppression du scrollbar horizontal forcé par les ombres */
section {
  overflow-x: hidden;
}
</style>