<template>
  <div class="relative w-full">
    <label
      class="absolute -top-2 left-2 inline-block bg-white px-1 text-xs font-medium text-gray-900"
    >
      {{ label }}
    </label>

    <button
      type="button"
      @click="isOpen = !isOpen"
      class="block w-full rounded-md border-0 py-2.5 pl-3 pr-10 text-gray-900 shadow-sm
             ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-blue-600
             sm:text-sm sm:leading-6 flex justify-between items-center"
    >
      <span>{{ selectedOptionLabel }}</span>
      <svg
        class="h-5 w-5 text-gray-400"
        viewBox="0 0 20 20"
        fill="currentColor"
        aria-hidden="true"
      >
        <path
          fill-rule="evenodd"
          d="M10 3a.75.75 0 01.53.22l3.5 3.5a.75.75 0 01-1.06 1.06L10 4.81
             7.03 7.78a.75.75 0 01-1.06-1.06l3.5-3.5A.75.75 0 0110 3zm-3.72
             9.28a.75.75 0 011.06 0L10 15.19l2.97-2.91a.75.75 0
             111.06 1.06l-3.5 3.5a.75.75 0 01-1.06 0l-3.5-3.5a.75.75
             0 010-1.06z"
          clip-rule="evenodd"
        />
      </svg>
    </button>

    <ul
      v-if="isOpen"
      class="absolute z-10 mt-1 max-h-60 w-full overflow-auto
             rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5
             focus:outline-none sm:text-sm"
    >
      <li
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)"
        :class="[
          'relative cursor-pointer select-none py-2 pl-3 pr-9',
          'transition-colors duration-200 ease-in-out', 
          modelValue === option.value 
            ? 'bg-[#103D92] text-white' 
            : 'text-gray-900 hover:bg-gray-100'
        ]"
      >
        <span
          :class="[
            'block truncate',
            modelValue === option.value ? 'font-semibold' : ''
          ]"
        >
          {{ option.label }}
        </span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  label: { type: String, required: true },
  options: { type: Array, required: true },
  modelValue: { type: String, required: true }
})

const emit = defineEmits(['update:modelValue'])
const isOpen = ref(false)

const selectedOptionLabel = computed(() => {
  const found = props.options.find(o => o.value === props.modelValue)
  return found ? found.label : 'Выберите...'
})

function selectOption(option) {
  emit('update:modelValue', option.value)
  isOpen.value = false
}
</script>
