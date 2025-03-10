<script setup lang="ts">
import Swal from "sweetalert2";

defineProps<{ msg: string }>()

const showAlert = (msg: string): void => {
  // Usando SweetAlert2
  Swal.fire({
    title: "Good job!",
    text: msg,
    icon: "success"
  });
};

</script>

<template>
  <div class="flex flex-col items-center">
    <h1 class="text-3xl font-bold underline">{{ msg }}</h1>
  
    <button type="button" class="bg-blue-700 text-white rounded-lg px-5" @click="showAlert(msg)">Hello world</button>
  </div>
</template>
