<!-- pages/index.vue -->
<template>
  <div class="p-10">
    <h1 class="text-4xl font-bold mb-4">[translate:Добро пожаловать в Secret Manager]</h1>
    <p class="text-lg text-gray-600">[translate:Выберите раздел в меню слева, чтобы начать работу.]</p>
    
    <div class="mt-8 grid grid-cols-1 md:grid-cols-2 gap-6">
      <NuxtLink to="/secrets" class="block p-6 bg-white border rounded-lg shadow hover:bg-gray-100">
        <h2 class="mb-2 text-2xl font-bold tracking-tight text-gray-900">Секреты</h2>
        <p class="font-normal text-gray-700">Управление вашими секретными данными</p>
      </NuxtLink>

      <NuxtLink to="/projects" class="block p-6 bg-white border rounded-lg shadow hover:bg-gray-100">
        <h2 class="mb-2 text-2xl font-bold tracking-tight text-gray-900">Проекты</h2>
        <p class="font-normal text-gray-700">Просмотр и управление проектами</p>
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
</script>
