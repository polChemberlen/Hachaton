<template>
  <div class="p-10">
    <h1 class="text-3xl">Это страница 1</h1>
    <p>Нажми кнопку, чтобы открыть форму</p>
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
