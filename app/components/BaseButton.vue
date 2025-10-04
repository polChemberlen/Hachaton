<template>
    <button class="rounded-md bg-[#103D92] px-3.5 py-2.5 text-sm font-semibold text-white
           shadow-sm hover:bg-blue-800 focus-visible:outline focus-visible:outline-2
           focus-visible:outline-offset-2 focus-visible:outline-blue-600" @click="$emit('click')">
        <slot />
    </button>
</template>

<script setup>
defineEmits(['click'])
</script>
