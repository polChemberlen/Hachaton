<template>

  <div class="flex-grow flex flex-col">
    <header class="p-10 pb-2">
      <RequestsHeader 
        :search-query="searchQuery"
        @update:searchQuery="$emit('update:searchQuery', $event)"
        @open-modal="$emit('update:isModalOpen', true)"
      />
    </header>

    <main class="flex-1 overflow-y-auto p-10 pt-0">
      <RequestsDataTable :search-query="searchQuery" />
    </main>
  </div>
</template>

<script setup>

defineProps({
  searchQuery: String
});

defineEmits(['update:searchQuery']);
</script>
