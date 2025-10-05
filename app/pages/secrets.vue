<template>
  <div class="flex-grow flex flex-col">

    <header class="p-10 pb-2">
      <SecretsHeader 
        :search-query="searchQuery"
        @update:searchQuery="searchQuery = $event"
        @open-modal="$emit('update:isModalOpen', true)"
      />
    </header>


    <main class="flex-1 overflow-y-auto p-10 pt-0">
      <DataTable :search-query="searchQuery" />
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue';

import SecretsHeader from '~/components/SecretsHeader.vue';
import DataTable from '~/components/DataTable.vue';


const searchQuery = ref('');


defineProps({
  isModalOpen: Boolean
});
defineEmits(['update:isModalOpen']);
</script>
