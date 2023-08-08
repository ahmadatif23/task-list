<script setup>
</script>

<template>
  <main class="w-full h-full flex flex-col items-center justify-center text-[#f7f9fd] text-center p-10">
    <h3 class="font-bold text-lg mb-4">Tasks List</h3>
    <h1 class="text-4xl font-semibold mb-6">Welcome Back!</h1>

    <RouterLink
      to="Tasks"
      class="appearance-none border border-white rounded-xl px-5 py-3 hover:bg-white/20 transition-all"
    >
      Kick Off a New Task
    </RouterLink>
  </main>
</template>
