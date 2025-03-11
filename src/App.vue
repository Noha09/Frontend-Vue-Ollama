<script setup lang="ts">
import { onMounted } from 'vue';
import { initModals } from 'flowbite';
import Sidebar from './components/Sidebar.vue';

// initialize components based on data attribute selectors
onMounted(() => {
  initModals();
});
</script>

<template>
  <Sidebar />
</template>