<template>
  <div class="p-10">
    <h1 class="text-3xl">Мои секреты</h1>
    <BaseButton @click="isModalOpen = true" class="mt-4">
      Создать новую заявку
    </BaseButton>

    <NewRequestModal
      v-if="isModalOpen"
      @close="isModalOpen = false"
    />
  </div>
</template>

<script setup>

const isModalOpen = ref(false)
</script>
