<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { initModals } from 'flowbite';
import Sidebar from './components/Sidebar.vue';

// Definimos la interfaz para los elementos del menú
interface MenuItem {
  id: string;
  label: string;
  icon: string;
  path?: string;
  isActive?: boolean;
}

// Creamos un array con los elementos del menú
const menuItems = ref<MenuItem[]>([
  {
    id: 'dashboard',
    label: 'Dashboard',
    icon: `<svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 22 21">
            <path d="M16.975 11H10V4.025a1 1 0 0 0-1.066-.998 8.5 8.5 0 1 0 9.039 9.039.999.999 0 0 0-1-1.066h.002Z"/>
            <path d="M12.5 0c-.157 0-.311.01-.565.027A1 1 0 0 0 11 1.02V10h8.975a1 1 0 0 0 1-.935c.013-.188.028-.374.028-.565A8.51 8.51 0 0 0 12.5 0Z"/>
          </svg>`,
    isActive: true
  },
  {
    id: 'newChat',
    label: 'Nuevo Chat',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 20.25c4.97 0 9-3.694 9-8.25s-4.03-8.25-9-8.25S3 7.444 3 12c0 2.104.859 4.023 2.273 5.48.432.447.74 1.04.586 1.641a4.483 4.483 0 0 1-.923 1.785A5.969 5.969 0 0 0 6 21c1.282 0 2.47-.402 3.445-1.087.81.22 1.668.337 2.555.337Z" />
          </svg>`,
    path: '/chat'
  },
  // Puedes añadir más elementos aquí
]);

// Almacenamos la ruta activa
const activePath = ref('/');

// Estado para controlar si el sidebar está colapsado
const isCollapsed = ref(false);

// Función para alternar el estado de colapso del sidebar
const toggleSidebar = () => {
  isCollapsed.value = !isCollapsed.value;
  // Opcional: guardar preferencia en localStorage
  localStorage.setItem('sidebarCollapsed', isCollapsed.value.toString());
};

// initialize components based on data attribute selectors
onMounted(() => {
  initModals();
  
  // Recuperar preferencia de colapso del localStorage (si existe)
  const savedCollapsedState = localStorage.getItem('sidebarCollapsed');
  if (savedCollapsedState !== null) {
    isCollapsed.value = savedCollapsedState === 'true';
  }
});
</script>

<template>
  <!-- Pasamos los elementos del menú, la ruta activa y el estado de colapso como props al componente Sidebar -->
  <Sidebar 
    :menuItems="menuItems" 
    :activePath="activePath" 
    :isCollapsed="isCollapsed"
    @toggleCollapse="toggleSidebar"
  />
  
  <!-- Contenido principal que se ajusta según el estado del sidebar -->
  <main class="p-4 transition-all duration-300" :class="[isCollapsed ? 'sm:ml-16' : 'sm:ml-64']">
    <div class="p-4 border-2 border-gray-200 border-dashed rounded-lg dark:border-gray-700">
      <div class="grid grid-cols-1 gap-4 mb-4">
        <div class="flex items-center justify-center h-24 rounded bg-gray-50 dark:bg-gray-800">
          <p class="text-2xl text-gray-400 dark:text-gray-500">
            Contenido principal
          </p>
        </div>
      </div>
    </div>
  </main>
</template>