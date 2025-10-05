<template>
    <div class="overflow-x-auto">

        <div v-if="filteredRows.length === 0" class="py-10 text-center text-gray-500 text-xl">
            Ничего не найдено
        </div>
        <table v-else class="min-w-[95%] border-collapse border-spacing-0">
            <thead>
                <tr class="border-b-2 border-[#103D92]">
                    <th class="p-4 pb-4 pt-2 font-normal text-left">
                        <div class="flex items-center justify-center mt-2">
                            <label class="relative flex items-center justify-center w-6 h-6">
                                <input type="checkbox" :checked="isAllSelected" :indeterminate.prop="isIndeterminate"
                                    @change="toggleAll"
                                    class="cursor-pointer peer appearance-none w-6 h-6 border-2 border-blue-900 rounded bg-white checked:border-blue-900 focus:ring-2 focus:ring-blue-400 transition-all" />
                                <svg v-if="!isIndeterminate"
                                    class="absolute left-0 top-0 w-6 h-6 pointer-events-none hidden peer-checked:block"
                                    viewBox="0 0 24 24" fill="none" stroke="#103D92" stroke-width="3"
                                    stroke-linecap="round" stroke-linejoin="round">
                                    <polyline points="20 6 9 17 4 12" />
                                </svg>
                                <svg v-if="isIndeterminate" class="absolute left-0 top-0 w-6 h-6 pointer-events-none"
                                    viewBox="0 0 24 24" fill="none" stroke="#103D92" stroke-width="3"
                                    stroke-linecap="round" stroke-linejoin="round">
                                    <line x1="6" y1="12" x2="18" y2="12" />
                                </svg>
                            </label>
                        </div>
                    </th>
                    <th class="px-4 py-2 font-bold text-left text-xl">&emsp;&emsp;&ensp;Имя</th>
                    <th class="px-4 py-2 font-bold text-left text-xl">Проект</th>
                    <th class="px-4 py-2 font-bold text-left text-xl">Последнее изменение</th>
                    <th class="px-4 py-2"></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="row in filteredRows" :key="row.id"
                    class="border-b-2 border-[#103D92] hover:bg-gray-100 transition duration-150">
                    <td class="px-4 py-4 text-center">
                        <label class="relative flex items-center justify-center w-6 h-6 mx-auto">
                            <input type="checkbox" :value="row.id" v-model="selectedRows"
                                class="cursor-pointer peer appearance-none w-6 h-6 border-2 border-blue-900 rounded bg-white checked:border-blue-900 focus:ring-2 focus:ring-blue-400 transition-all" />
                            <svg class="absolute left-0 top-0 w-6 h-6 pointer-events-none hidden peer-checked:block"
                                viewBox="0 0 24 24" fill="none" stroke="#103D92" stroke-width="3" stroke-linecap="round"
                                stroke-linejoin="round">
                                <polyline points="20 6 9 17 4 12" />
                            </svg>
                        </label>
                    </td>
                    <td class="px-4 py-4">
                        <div class="flex items-center gap-2">
                    
                            <svg width="41" height="40" viewBox="0 0 41 40" fill="none"
                                xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                                <rect width="40" height="40" transform="matrix(-1 0 0 1 40.377 0)"
                                    fill="url(#pattern0_21_321)" />
                                <defs>
                                    <pattern id="pattern0_21_321" patternContentUnits="objectBoundingBox" width="1"
                                        height="1">
                                        <use xlink:href="#image0_21_321" transform="scale(0.02)" />
                                    </pattern>
                                    <image id="image0_21_321" width="50" height="50" preserveAspectRatio="none"
                                        xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAADG0lEQVR4nO2ZTUtVQRjHf+ZG0zaBl9q1UqFN61TwJTdBCyn6DqXLNNpoSkGlHyGoTfU1olKhXEQKvWmvGw3aVWTUPTHwHxgu59w75zpzPDf6w3APz5x55vmfmedl5oIf2oEhYAlYBXaAX2o7ki0Cg3q3dOgEZmRs4tnMu9NAByXBOeCTY+BL4AYwBvQDXWr9kpm+V877H4GJ/STQBlwFqjLoGTCaY/xJ4InGVkXwAAXjAPBARpj9f0HE8sKMuSgdRte9JvU0jeua+CswzN4xLF1G5wIF+kRVXzEECYth6awW4TOdjmOb7VSLg/qimzJqC5jXOB9MOgEgajSb0URPU/ayMXYlI9Que5JpU9AwYy5F4kC7kydGUvrn1fdO0atL4fa95HOe84zq/e1YUWzIyRNp2FR/bQgek/xtjrlsnhkgApak3MT7NOyqv7tGfkjynznmuqUx5jc4VqXcfOE0bGWsyLjkb3LMNe74VnB8kfLejH7rI8YnTmlljEEfJJ/NMVef4yfBsSvlZqukoVNfMC1qPc4ZTpvZjsGIIGPn5Ni7+p1iO..." />
                                </defs>
                            </svg>

               
                            <div>
                                <div class="text-blue-700 font-bold leading-tight text-xl">{{ row.name }}</div>
                                <div class="text-black text-sm leading-tight text-xl">{{ row.secret }}</div>
                            </div>
                        </div>
                    </td>

                    <td class="px-4 py-2 text-xl">{{ row.project }}</td>
                    <td class="px-4 py-2 text-xl">{{ row.date }}</td>
                    <td class="px-4 py-2 text-center">
                        <button class="text-3xl text-gray-500">&#8942;</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
    searchQuery: { type: String, default: '' }
});

const allRows = ref([
    { id: 1, name: 'KEYNAME', secret: '***********************', project: 'Проект А', date: '1 января 1970г' },
    { id: 2, name: 'DB_PASS', secret: '***********************', project: 'Проект B', date: '2 февраля 1971г' },
    { id: 3, name: 'API_TOKEN', secret: '***********************', project: 'Проект C', date: '3 марта 1972г' },

]);

const selectedRows = ref([]);

const filteredRows = computed(() => {
    if (!props.searchQuery) return allRows.value;
    const q = props.searchQuery.toLowerCase();
    return allRows.value.filter(r => r.name.toLowerCase().includes(q));
});

const isAllSelected = computed(() => {
    const ids = filteredRows.value.map(r => r.id);
    return ids.length > 0 && ids.every(id => selectedRows.value.includes(id));
});

const isIndeterminate = computed(() => {
    const ids = filteredRows.value.map(r => r.id);
    const sel = selectedRows.value.filter(id => ids.includes(id));
    return sel.length > 0 && sel.length < ids.length;
});

const toggleAll = event => {
    const ids = filteredRows.value.map(r => r.id);
    if (event.target.checked) {
        selectedRows.value = Array.from(new Set([...selectedRows.value, ...ids]));
    } else {
        selectedRows.value = selectedRows.value.filter(id => !ids.includes(id));
    }
};
</script>
