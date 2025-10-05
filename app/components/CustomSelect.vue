<template>
  <div class="relative w-full">
    <label class="absolute -top-2 left-2 inline-block bg-white px-1 text-xs font-medium text-gray-900">
      {{ label }}
    </label>

    <button type="button" @click="isOpen = !isOpen" class="block w-full rounded-md border-0 py-2.5 pl-3 pr-5 text-gray-900 shadow-sm
             ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-blue-600
             sm:text-sm sm:leading-6 flex justify-between items-center">
      <span>{{ selectedOptionLabel }}</span>
      <svg width="16" height="16" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink">
        <rect width="32" height="32" fill="url(#pattern0_160_1111)" />
        <defs>
          <pattern id="pattern0_160_1111" patternContentUnits="objectBoundingBox" width="1" height="1">
            <use xlink:href="#image0_160_1111" transform="scale(0.0111111)" />
          </pattern>
          <image id="image0_160_1111" width="90" height="90" preserveAspectRatio="none"
            xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFoAAABaCAYAAAA4qEECAAAACXBIWXMAAAsTAAALEwEAmpwYAAACx0lEQVR4nO3bPW8TMRgHcCNeixRsXycgYmMpYyUUiJ2s3ZgywMLLF+AjlKEDAqXN4yCkTIBUJMTYTnwExNANhm4MRZQ3iQF1AIIuiVQhopDc+Rzb9/9JN/vxI9/5+feFMQAAAAAAAAAAAAAAAAAAAAAAACiVpdUTQtO6UObb6Nmo1toLrGSqtfZCuneh6eugD5rW095YW2DQZG36fz/0JmlSlZVEUmufT/f8bx9M29oiQtHnMQv0uaIPstG9wiKX1KnGldkb1wOhzCdrC41d4HChA16nOyxSUpnrXJsfk3rgptGHT48t946zWLReHhXa3J9m764bnZ7uV1w9lixwyWU6w7XZmnbf7hs9aDbtyvqjSyxQlUbnIlfm7Sx7nk+j00tSm+9C0zUWGKloZTi2zbZfawXMuvBo/PvNNd1jrH+EBUA0uneFop9Z9mqtCK7ofbZmD0bA5z6Hm7S2tMas+xPafLFWDNdmLUchfV/DzYQQMstncs1eRc3VY1yZzVwFKbPnU7iZGEKm39Nm2huvvmPCo3AjG90b/wshc79/st7MwodwM0MI8WKiGs6a9C5Xs5XbcDMMIbSdr2baTRQtuarZauHSQbjJEkLmfTCCexWlrU9dEZdeLJeLsHF5q+5t5hMb45JQ9OLscu907mJW6CRX5mnOU7wv9EaD+WjxavecUPQ65wZ3ZL1zIeQa3Gg+OcU1PZvHaUp8eqtccR1upKf3hBNOwk3L/8kn+HCThBpCQgo3lQDTqRste694VCGkKFybW+lFl6NBv0ZP1lN8IHTnJiuDxMYYFlsIKcqinWARWQjxO9z0owsh3oYbHWEIKYq0M0nEFUKKUrExG8cWQrwNNyrGEOJfuOlFHUKKIqf9iZyPvwmJMNzsly6EzCHc7JQ3hBT7H1EPhyeYPgpFD3z+40kAAAAAAAAAAAAAAAAAAAAAYEH4A9D4eoBJg1GUAAAAAElFTkSuQmCC" />
        </defs>
      </svg>

    </button>

    <ul v-if="isOpen" class="absolute z-10 mt-1 max-h-60 w-full overflow-auto
             rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5
             focus:outline-none sm:text-sm">
      <li v-for="option in options" :key="option.value" @click="selectOption(option)" :class="[
        'relative cursor-pointer select-none py-2 pl-3 pr-9',
        'transition-colors duration-200 ease-in-out',
        modelValue === option.value
          ? 'bg-[#103D92] text-white'
          : 'text-gray-900 hover:bg-gray-100'
      ]">
        <span :class="[
          'block truncate',
          modelValue === option.value ? 'font-semibold' : ''
        ]">
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
