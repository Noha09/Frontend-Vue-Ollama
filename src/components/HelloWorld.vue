<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>

  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</template>
