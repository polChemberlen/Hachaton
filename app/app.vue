<template>
  <div class="flex h-screen bg-gray-50">
    <AppSidebar />

    <div class="flex-1 flex flex-col overflow-hidden">

      <NuxtPage 
        :search-query="searchQuery" 
        :is-modal-open="isModalOpen"
        @update:search-query="searchQuery = $event"
        @update:is-modal-open="isModalOpen = $event"
      />
    </div>

    <NewRequestModal
      v-if="isModalOpen"
      @close="isModalOpen = false"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const searchQuery = ref('');
const isModalOpen = ref(false);
</script>
