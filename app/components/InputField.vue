<template>
    <div class="relative">
        <label :for="id" class="absolute -top-2 left-2 inline-block bg-white px-1 text-xs font-medium text-gray-900">
            {{ label }}
        </label>
        <input :type="type" :id="id" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"
            :placeholder="placeholder" class="block w-full rounded-md border-0 py-2.5 px-3 text-gray-900 shadow-sm
             ring-1 ring-inset ring-gray-300 placeholder:text-gray-400
             focus:ring-10 focus:ring-inset focus:ring-[#103D92] sm:text-sm sm:leading-6" />
    </div>
</template>

<script setup>
defineProps({
    id: { type: String, required: true },
    label: { type: String, required: true },
    modelValue: { type: String, required: true },
    type: { type: String, default: 'text' },
    placeholder: { type: String, default: '' }
})

defineEmits(['update:modelValue'])
</script>
