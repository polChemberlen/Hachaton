<template>
    <div class="overflow-x-auto">
        <table class="min-w-[95%] border-collapse border-spacing-0">
            <thead>
                <tr class="border-b-2 border-[#103D92]">
                    <th class="p-4 pb-4 pt-2 font-normal text-left">
                        <div class="flex items-center justify-center mt-2">
                            <label class="relative flex items-center justify-center w-6 h-6">
                                <input type="checkbox" :checked="isAllSelected" :indeterminate="isIndeterminate"
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
                    <th class="px-4 py-2 font-bold text-center text-xl">Номер</th>
                    <th class="px-4 py-2 font-bold text-left text-xl">Имя</th>
                    <th class="px-4 py-2 font-bold text-left text-xl">Статус</th>
                    <th class="px-4 py-2 font-bold text-left text-xl">Дата</th>
                    <button class="ml-2 text-3xl px-4 py-2 text-center"></button>
                </tr>
            </thead>
            <tbody>
                <tr v-for="row in rows" :key="row.id"
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
                    <td class="px-4 py-2 text-xl">{{ row.number }}</td>
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
                                        xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAADG0lEQVR4nO2ZTUtVQRjHf+ZG0zaBl9q1UqFN61TwJTdBCyn6DqXLNNpoSkGlHyGoTfU1olKhXEQKvWmvGw3aVWTUPTHwHxgu59w75zpzPDf6w3APz5x55vmfmedl5oIf2oEhYAlYBXaAX2o7ki0Cg3q3dOgEZmRs4tnMu9NAByXBOeCTY+BL4AYwBvQDXWr9kpm+V877H4GJ/STQBlwFqjLoGTCaY/xJ4InGVkXwAAXjAPBARpj9f0HE8sKMuSgdRte9JvU0jeua+CswzN4xLF1G5wIF+kRVXzEECYth6awW4TOdjmOb7VSLg/qimzJqC5jXOB9MOgEgajSb0URPU/ayMXYlI9Que5JpU9AwYy5F4kC7kydGUvrn1fdO0atL4fa95HOe84zq/e1YUWzIyRNp2FR/bQgek/xtjrlsnhkgApak3MT7NOyqv7tGfkjynznmuqUx5jc4VqXcfOE0bGWsyLjkb3LMNe74VnB8kfLejH7rI8YnTmlljEEfJJ/NMVef4yfBsSvlZqukoVNfMC1qPc4ZTpvZjsGIIGPn5Ni7+p1tIidYIt+IgJ0GWysk+pxQHhwrDZw9JKyzP4qhfLFB+I0xlylOg2OwQUIMidea68x+lCihYCsB09aBChEwXadoDAGjc01zfI9JpkMldqKTXWhMOdHqmEhEIzMR6WA14hx5T0tWiU1mIeJR91pNX1QybcB95/Jhcg+XD1POStzN0BOdzGXgjyZYy3kdNOY4ts91UA/wwkkBR4ngMzYAJMoBN5Wd+1UFd+t5XGcMmycSVcf18kXFWYHoPtOhM/Z2jitTe3CqV1Baw9eLJIO2xoAMXBYxUwX/AD4DD1V+bHgakmV0xZFvxCLjgzz7Pevdntg+44v/ZGgBMlntnyFDK5FJQxoRg5Yjk0UkzegjZSZTj0hLkfEJAJU6SdMm3udF/xPWDJFGZGzZdIKSwTcA2G12W7IrlAx5A8DZmHdkRQaAXhWuv4HDlAjNBAD7fJ4SwTcApFULdyg5kozt5q5MtP9bivKb4869giFVaiQ5Q3JpkTRoLUHCwJvEXwoCq1km7r2HAAAAAElFTkSuQmCC" />
                                </defs>
                            </svg>
                            <div class="flex flex-col justify-center">
                                <div class="text-blue-700 font-bold leading-tight text-xl">{{ row.name }}</div>
                                <div class="text-black text-sm leading-tight text-xl">{{ row.secret }}</div>
                            </div>
                        </div>
                    </td>
                    <td class="px-4 py-2 text-xl">{{ row.status }}</td>
                    <td class="px-4 py-2 flex items-center justify-between text-xl h-[90px]">
                        <span>{{ row.date }}</span>

                    </td>
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

const rows = [
    { id: 1, number: '44-0410', name: 'KEYNAME', secret: '***********************', status: 'Одобрено', date: '1 января 1970г' },
    { id: 2, number: '45-0410', name: 'KEYNAME', secret: '***********************', status: 'На рассмотрении', date: '1 января 1970г' },
];

const selectedRows = ref([]);

const isAllSelected = computed(() => {
    return rows.length > 0 && selectedRows.value.length === rows.length;
});

const isIndeterminate = computed(() => {
    return selectedRows.value.length > 0 && selectedRows.value.length < rows.length;
});

const toggleAll = (event) => {
    if (event.target.checked) {
        selectedRows.value = rows.map(row => row.id);
    } else {
        selectedRows.value = [];
    }
};

</script>
