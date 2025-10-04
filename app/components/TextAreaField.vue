<template>
  <div class="relative h-full">
    <label 
      :for="id" 
      class="absolute -top-2 left-2 inline-block bg-white px-1 text-xs font-medium text-gray-900"
    >
      {{ label }}
    </label>
    <textarea 
      :id="id" 
      :value="modelValue" 
      @input="$emit('update:modelValue', $event.target.value)" 
      rows="5" 
      class="
        block w-full h-full rounded-md border-0 py-2.5 px-3 shadow-sm 
        text-gray-900 <!-- Возвращаем черный цвет текста -->
        ring-1 ring-inset ring-gray-300 
        placeholder:text-gray-400 
        focus:ring-2 focus:ring-inset focus:ring-[#103D92] 
        sm:text-sm sm:leading-6 
        resize-none
      " 
      :placeholder="placeholder"
    ></textarea>
  </div>
</template>

<script setup>
defineProps({
  id: { type: String, required: true },
  label: { type: String, required: true },
  modelValue: { type: String, required: true },
  placeholder: { type: String, default: '' }
})

defineEmits(['update:modelValue'])
</script>
