<template>
  <div class="max-w-2xl mx-auto">
    <div class="bg-bg-card rounded-xl p-6 border border-border">
      <h3 class="text-xl font-display font-semibold text-text-primary mb-5">
        Envíame un mensaje
      </h3>
      
      <form @submit.prevent="handleSubmit" class="space-y-4">
        <div>
          <input 
            v-model="form.name"
            type="text" 
            name="name"
            required
            class="w-full px-4 py-2.5 bg-bg-tertiary border border-border rounded-lg focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary text-text-primary text-sm"
            placeholder="Tu nombre"
          />
        </div>
        
        <div>
          <input 
            v-model="form.email"
            type="email" 
            name="email"
            required
            class="w-full px-4 py-2.5 bg-bg-tertiary border border-border rounded-lg focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary text-text-primary text-sm"
            placeholder="Tu email"
          />
        </div>
        
        <div>
          <textarea 
            v-model="form.message"
            name="message"
            required
            rows="5"
            class="w-full px-4 py-2.5 bg-bg-tertiary border border-border rounded-lg focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary text-text-primary text-sm resize-none"
            placeholder="Cuéntame sobre tu proyecto..."
          ></textarea>
        </div>
        
        <button 
          type="submit"
          class="w-full bg-primary hover:bg-primary-dark text-white font-semibold py-2.5 rounded-lg transition-all disabled:opacity-50"
          :disabled="loading"
        >
          {{ loading ? 'Enviando...' : 'Enviar mensaje' }}
        </button>
        
        <div v-if="success" class="bg-success/10 border border-success text-success px-4 py-2 rounded-lg text-center text-sm">
          ¡Mensaje enviado con éxito! Te responderé pronto.
        </div>
        
        <div v-if="error" class="bg-red-500/10 border border-red-500 text-red-400 px-4 py-2 rounded-lg text-center text-sm">
          {{ error }}
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const form = ref({
  name: '',
  email: '',
  message: ''
});

const loading = ref(false);
const success = ref(false);
const error = ref('');

// Tu endpoint de Formspree
const FORMSPREE_ENDPOINT = 'https://formspree.io/f/xeepekrg';

const handleSubmit = async () => {
  loading.value = true;
  success.value = false;
  error.value = '';
  
  try {
    const response = await fetch(FORMSPREE_ENDPOINT, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
      },
      body: JSON.stringify({
        name: form.value.name,
        email: form.value.email,
        message: form.value.message,
        _subject: `Nuevo mensaje de ${form.value.name} - Portfolio SamuDev`
      })
    });
    
    if (response.ok) {
      success.value = true;
      form.value = { name: '', email: '', message: '' };
      setTimeout(() => {
        success.value = false;
      }, 5000);
    } else {
      const data = await response.json();
      if (data.errors) {
        error.value = data.errors.map(e => e.message).join(', ');
      } else {
        error.value = 'Hubo un error al enviar el mensaje. Intenta de nuevo.';
      }
    }
  } catch (err) {
    console.error('Error:', err);
    error.value = 'Error de conexión. Por favor, intenta de nuevo.';
  } finally {
    loading.value = false;
  }
};
</script>