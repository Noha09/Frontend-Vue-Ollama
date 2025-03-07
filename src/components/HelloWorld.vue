<script setup lang="ts">

defineProps<{ msg: string }>()

import Swal from "sweetalert2";

const showAlert = () => {
  // Usando SweetAlert2
  Swal.fire("Hello Vue world!!!");
};

</script>

<template>
  <h1>{{ msg }}</h1>

  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
  
  <button @click="showAlert">Hello world</button>
</template>