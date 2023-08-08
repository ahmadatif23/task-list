<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="flex justify-center items-center w-screen h-screen bg-sky-950">
    <div class="max-w-3xl w-full h-full">
      <RouterView />
    </div>
  </div>
</template>
