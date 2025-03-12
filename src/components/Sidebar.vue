<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// Definimos la interfaz para los elementos del menú
interface MenuItem {
  id: string;
  label: string;
  icon: string;
  path?: string;
  isActive?: boolean;
}

// Declaramos las props para recibir los elementos del menú y el estado de colapso
defineProps<{
  menuItems: MenuItem[];
  activePath?: string;
  isCollapsed: boolean;
}>();

// Emitimos eventos que el componente padre puede escuchar
const emit = defineEmits(['toggleCollapse']);

// Estado para almacenar si estamos en una pantalla móvil
const isMobileScreen = ref(false);

// Función para verificar el tamaño de pantalla
const checkScreenSize = () => {
  if (typeof window !== 'undefined') {
    isMobileScreen.value = window.innerWidth < 640;
  }
};

// Configurar listeners al montar el componente
onMounted(() => {
  checkScreenSize(); // Comprobar tamaño inicial
  window.addEventListener('resize', checkScreenSize); // Añadir listener para cambios de tamaño
});

// Limpiar listeners al desmontar el componente
onUnmounted(() => {
  window.removeEventListener('resize', checkScreenSize);
});

// Función para alternar el estado de colapso
const toggleSidebar = () => {
  emit('toggleCollapse');
};

// Función para determinar si un elemento del menú está activo
const isMenuItemActive = (menuItem: MenuItem, activePath?: string) => {
  if (menuItem.isActive !== undefined) return menuItem.isActive;
  
  if (activePath && menuItem.path) {
    return menuItem.path === activePath;
  }
  
  return false;
};
</script>

<template>
  <!-- Botón para dispositivos móviles -->
  <button data-drawer-target="default-sidebar" data-drawer-toggle="default-sidebar" aria-controls="default-sidebar" type="button" class="inline-flex items-center p-2 mt-2 ms-3 text-sm text-gray-500 rounded-lg sm:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600">
    <span class="sr-only">Open sidebar</span>
    <svg class="w-6 h-6" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
      <path clip-rule="evenodd" fill-rule="evenodd" d="M2 4.75A.75.75 0 012.75 4h14.5a.75.75 0 010 1.5H2.75A.75.75 0 012 4.75zm0 10.5a.75.75 0 01.75-.75h7.5a.75.75 0 010 1.5h-7.5a.75.75 0 01-.75-.75zM2 10a.75.75 0 01.75-.75h14.5a.75.75 0 010 1.5H2.75A.75.75 0 012 10z"></path>
    </svg>
  </button>
  
  <aside 
    id="default-sidebar" 
    class="fixed top-0 left-0 z-40 h-screen transition-all duration-300" 
    :class="[
      isCollapsed ? 'w-16' : 'w-64',
      'sm:translate-x-0',
      { '-translate-x-full': !isCollapsed && isMobileScreen }
    ]" 
    aria-label="Sidebar"
  >
    <div class="h-full relative px-3 py-4 overflow-y-auto bg-gray-50 dark:bg-gray-800">
      <!-- Botón para colapsar/expandir sidebar (visible en escritorio) -->
      <button 
        @click="toggleSidebar" 
        class="absolute -right-4 top-10 bg-gray-200 dark:bg-gray-700 p-1 rounded-full shadow hover:bg-gray-300 dark:hover:bg-gray-600 focus:outline-none transition-all duration-200"
        :class="{ 'rotate-180': isCollapsed }"
      >
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-5 h-5 text-gray-500 dark:text-gray-400">
          <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
        </svg>
      </button>

      <ul class="space-y-2 font-medium">
        <li v-for="item in menuItems" :key="item.id">
          <!-- Si hay una ruta, renderizamos un enlace, de lo contrario, un elemento de texto -->
          <a 
            v-if="item.path" 
            :href="item.path" 
            class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group"
            :class="{ 'bg-gray-100 dark:bg-gray-700': isMenuItemActive(item, activePath) }"
          >
            <!-- Renderizamos el icono de manera dinámica usando v-html -->
            <span v-html="item.icon" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 min-w-6"></span>
            <span v-if="!isCollapsed" class="flex-1 ms-3 whitespace-nowrap transition-opacity duration-300">{{ item.label }}</span>
          </a>
          
          <p 
            v-else 
            class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white"
            :class="{ 'bg-gray-100 dark:bg-gray-700': isMenuItemActive(item, activePath) }"
          >
            <span v-html="item.icon" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 min-w-6"></span>
            <span v-if="!isCollapsed" class="ms-3 transition-opacity duration-300">{{ item.label }}</span>
          </p>
        </li>
      </ul>
    </div>
  </aside>
</template>