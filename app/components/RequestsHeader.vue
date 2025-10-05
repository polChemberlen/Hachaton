<template>
    <div class="flex justify-between items-center">
        <h1 class="text-4xl font-bold text-gray-800">Заявки</h1>
        <div class="flex items-center space-x-4">

            <SearchInput :model-value="searchQuery" @update:model-value="$emit('update:searchQuery', $event)" />

            <BaseButton @click="$emit('open-modal')">
                Запросить
            </BaseButton>

            <button class=" p-2 rounded-full">
                <svg width="40" height="40" viewBox="0 0 70 70" fill="none" xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink">
                    <g clip-path="url(#clip0_40_475)">
                        <path
                            d="M35 69.5C54.0538 69.5 69.5 54.0538 69.5 35C69.5 15.9462 54.0538 0.5 35 0.5C15.9462 0.5 0.5 15.9462 0.5 35C0.5 54.0538 15.9462 69.5 35 69.5Z"
                            fill="#103D92" stroke="#103D92" />
                        <path
                            d="M15 13.5L57 12.5L63 55L53 65C53 65 49.5 67 49 67C48.5 67 40.5 68.5 43 69C36.2906 69.067 28.5 68.5 23 67.5C22 67.5 21.2517 66.5599 20.5 66.5C20.1427 66.4715 19.755 66.1966 19.3839 65.9419L18.5 65.5C15.9377 65.2829 12 60.5 12 60.5L15 13.5Z"
                            fill="url(#pattern0_40_475)" />
                        <path
                            d="M35 69.5C54.0538 69.5 69.5 54.0538 69.5 35C69.5 15.9462 54.0538 0.5 35 0.5C15.9462 0.5 0.5 15.9462 0.5 35C0.5 54.0538 15.9462 69.5 35 69.5Z"
                            stroke="#103D92" />
                    </g>
                    <defs>
                        <pattern id="pattern0_40_475" patternContentUnits="objectBoundingBox" width="1" height="1">
                            <use xlink:href="#image0_40_475"
                                transform="matrix(0.0228759 0 0 0.020647 -0.235294 -0.0442436)" />
                        </pattern>
                        <clipPath id="clip0_40_475">
                            <rect width="70" height="70" fill="white" />
                        </clipPath>
                        <image id="image0_40_475" width="60" height="60" preserveAspectRatio="none"
                            xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADwAAAA8CAYAAAA6/NlyAAAACXBIWXMAAAsTAAALEwEAmpwYAAACAklEQVR4nO3aPWsUQRwH4BGjjUQhYKEmYpFvYGWlYCVqsBHRUivNJYofQfwCWim+gY2idaK9L42VlfEFBbUPyQUMmvDImilCCOZyN5vMknlg4Vj2hvkxszv/m70QiqIoii0OBzGGl5jCXDym4rkWhkLT4QDuYsHaFvEMh0IT4Qza1m8WI6FJcDWOWLeq746HBo3sYg9hl4fOe6Qx2OU0/t/03h9yhYfSuxcyXnoWaghctTkYcoNx9RkNucGLGgNPhNzgc42Bp0JupH06r9QOuVGzkBtbMHC7xrwzITf4WGPgDyE3tuCy1Kox8OWQGwzVVFr+ybK0rOB+DYHvhMy3dGYThp3BvpAznEg0tasNgNOhCSz9cup1i2csNAlGupze1TQ+FZoIe3ErPmk7GdXH2d+z69jrGsVkVTXFMrQdP0/gSrZLT1EURVE0BPbgAp7jCQa6aGMAT2Mb57E75AR9OBeLivkV1dMPXMSODtrZiUv4uaKN+VicnMX2jUm1CvTjGr51UDZ+jyXmSQxjVzyG47nb8Zq1fI3vnvvDBo/odUzbPNOxD311hz2Md/LxHkfqCLoNNxO92U+t6tONqo8pwz6SvwdJQlv6f1VTtFIE/qI5PqUI/EtzzKUI/FZzvEoR+HiHe1Kb7TeO9hx4Weg3q5SOOaj69BrH/nW2KIqiKIqQq79lyoeCP2qbHgAAAABJRU5ErkJggg==" />
                    </defs>
                </svg>


            </button>

        </div>
    </div>
</template>

<script setup>
import SearchInput from './SearchInput.vue'
import BaseButton from './BaseButton.vue'

defineProps({
    searchQuery: String
})
defineEmits(['update:searchQuery', 'open-modal'])
</script>
