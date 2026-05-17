<template>
  <div>
    <!-- Tech Skills - Cards con animaciones -->
    <div class="mb-20">
      <h3 class="text-xl font-semibold text-text-primary text-center mb-12">
        Desarrollo <span class="gradient-text">Web & Tecnologías</span>
      </h3>
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-5">
        <div 
          v-for="(skill, index) in techSkills" 
          :key="skill.name" 
          class="skill-card bg-bg-card rounded-2xl p-5 text-center border border-border hover:border-primary cursor-pointer group"
          :style="{ animationDelay: `${index * 0.05}s` }"
        >
          <div class="icon-wrapper mb-4 inline-block">
            <img 
              :src="skill.icon" 
              class="w-14 h-14 mx-auto transition-transform duration-300 group-hover:scale-110 group-hover:rotate-3" 
              :alt="skill.name" 
            />
          </div>
          <h4 class="font-bold text-text-primary text-base">{{ skill.name }}</h4>
        </div>
      </div>
    </div>

    <!-- Roblox & Lua Section -->
    <div class="mb-20">
      <h3 class="text-xl font-semibold text-text-primary text-center mb-12">
        Roblox <span class="gradient-text">Studio</span> & Lua
      </h3>
      
      <div class="bg-gradient-to-br from-bg-card to-bg-tertiary rounded-2xl p-6 border border-border hover:border-primary transition-all duration-500">
        <div class="flex items-center justify-center gap-8 mb-8 flex-wrap">
          <div class="text-center group">
            <div class="w-20 h-20 bg-bg-tertiary rounded-2xl flex items-center justify-center mx-auto group-hover:scale-110 transition-transform duration-300">
              <img 
                src="https://raw.githubusercontent.com/devicons/devicon/master/icons/roblox/roblox-original.svg" 
                class="w-12 h-12" 
                alt="Roblox Studio"
                @error="handleRobloxIconError"
              />
            </div>
            <p class="text-sm font-semibold text-text-primary mt-2">Roblox Studio</p>
          </div>
          <div class="text-3xl font-bold gradient-text">✦</div>
          <div class="text-center group">
            <div class="w-20 h-20 bg-bg-tertiary rounded-2xl flex items-center justify-center mx-auto group-hover:scale-110 transition-transform duration-300">
              <img 
                src="https://raw.githubusercontent.com/devicons/devicon/master/icons/lua/lua-original.svg" 
                class="w-12 h-12" 
                alt="Lua"
              />
            </div>
            <p class="text-sm font-semibold text-text-primary mt-2">Lua</p>
          </div>
        </div>
        
        <div class="grid md:grid-cols-2 gap-8">
          <!-- Conocimientos en Lua -->
          <div>
            <h4 class="font-bold text-text-primary mb-4 flex items-center gap-2">
              <span class="text-primary">📚</span> Conocimientos en Lua
            </h4>
            <div class="space-y-3">
              <div v-for="item in luaKnowledge" :key="item" class="flex items-start gap-2 text-sm text-text-secondary group/item hover:translate-x-1 transition-transform">
                <span class="text-primary mt-0.5">▹</span> 
                <span>{{ item }}</span>
              </div>
            </div>
          </div>
          
          <!-- Conocimientos en Roblox -->
          <div>
            <h4 class="font-bold text-text-primary mb-4 flex items-center gap-2">
              <span class="text-primary">🎮</span> Conocimientos en Roblox Studio
            </h4>
            <div class="space-y-3">
              <div v-for="item in robloxKnowledge" :key="item" class="flex items-start gap-2 text-sm text-text-secondary group/item hover:translate-x-1 transition-transform">
                <span class="text-primary mt-0.5">▹</span> 
                <span>{{ item }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Aprendizaje actual -->
        <div class="mt-8 pt-6 border-t border-border">
          <div class="flex items-center justify-between flex-wrap gap-4">
            <div class="flex items-center gap-3">
              <span class="text-yellow-500 text-xl">⚡</span>
              <span class="text-sm text-text-secondary">Actualmente profundizando en:</span>
            </div>
            <div class="flex flex-wrap gap-2">
              <span class="px-3 py-1 bg-primary/10 text-primary text-xs rounded-full">Sistemas de guardado</span>
              <span class="px-3 py-1 bg-primary/10 text-primary text-xs rounded-full">Optimización avanzada</span>
              <span class="px-3 py-1 bg-primary/10 text-primary text-xs rounded-full">APIs de Roblox</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Soft Skills -->
    <div>
      <h3 class="text-xl font-semibold text-text-primary text-center mb-12">
        Soft <span class="gradient-text">Skills</span>
      </h3>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
        <div 
          v-for="(skill, index) in softSkills" 
          :key="skill.name" 
          class="soft-skill-card bg-bg-card rounded-xl p-4 text-center border border-border hover:border-primary transition-all duration-300 hover:-translate-y-1 cursor-pointer"
          :style="{ animationDelay: `${index * 0.05}s` }"
        >
          <div class="text-3xl mb-2 inline-block transition-transform duration-300 group-hover:scale-110">{{ skill.icon }}</div>
          <h4 class="font-semibold text-text-primary text-sm">{{ skill.name }}</h4>
          <p class="text-xs text-text-tertiary mt-1">{{ skill.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const techSkills = [
  { name: 'HTML5', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg' },
  { name: 'CSS3', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg' },
  { name: 'JavaScript', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg' },
  { name: 'TypeScript', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg' },
  { name: 'Python', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg' },
  { name: 'Vue.js', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg' },
  { name: 'Astro', icon: 'https://avatars.githubusercontent.com/u/44914786?s=200&v=4' },
  { name: 'Tailwind', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg' }
];

const luaKnowledge = [
  'Sintaxis y fundamentos de Lua',
  'Programación orientada a objetos en Lua',
  'Manejo de tablas y metatables',
  'Funciones y closures',
  'Módulos y organización de código',
  'Depuración y manejo de errores'
];

const robloxKnowledge = [
  'Scripting con Lua en Roblox',
  'Creación de GUIs básicas',
  'Manejo de eventos (RemoteEvents)',
  'Trabajo con instancias y propiedades',
  'Sistemas de física básica',
  'Conocimiento del ecosistema Roblox'
];

const softSkills = [
  { name: 'Trabajo en Equipo', icon: '🤝', description: 'Colaboración efectiva' },
  { name: 'Comunicación', icon: '💬', description: 'Clara y directa' },
  { name: 'Resolución', icon: '🧩', description: 'Problemas complejos' },
  { name: 'Adaptabilidad', icon: '🔄', description: 'Aprendizaje rápido' },
  { name: 'Creatividad', icon: '🎨', description: 'Soluciones únicas' },
  { name: 'Autodidacta', icon: '📖', description: 'Aprendizaje continuo' },
  { name: 'Atención al detalle', icon: '🔍', description: 'Código limpio' },
  { name: 'Organización', icon: '📋', description: 'Metodologías ágiles' }
];

const handleRobloxIconError = (event) => {
  event.target.src = 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/roblox/roblox-original.svg';
  event.target.onerror = null;
};
</script>

<style scoped>
.skill-card {
  animation: fadeInUp 0.5s ease-out forwards;
  opacity: 0;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.skill-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 25px -12px rgba(59, 130, 246, 0.2);
}

.skill-card:hover .icon-wrapper img {
  transform: scale(1.1) rotate(3deg);
}

.soft-skill-card {
  animation: fadeInUp 0.5s ease-out forwards;
  opacity: 0;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>