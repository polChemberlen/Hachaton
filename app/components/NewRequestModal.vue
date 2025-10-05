<template>
    <div class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50"
        @click.self="!isSubmitted && $emit('close')">
        <div class="bg-white p-8 rounded-lg shadow-2xl w-full max-w-2xl">


            <div v-if="isSubmitted" class="text-center py-8">
                <h2 class="mt-4 text-2xl font-bold text-center text-gray-800">Заявка отправлена!</h2>
                <p class="mt-2 text-sm text-gray-600">Ваш запрос принят в обработку.</p>
                <div class="mt-6">
                    <BaseButton @click="$emit('close')">
                        Закрыть
                    </BaseButton>
                </div>
            </div>


            <div v-else>
                <h2 class="text-2xl font-bold mb-8 text-center text-gray-800">Новая заявка</h2>
                <form @submit.prevent="submitForm">
                    <div class="grid grid-cols-2 gap-x-8">
                        <!-- Левая колонка -->
                        <div class="flex flex-col space-y-4">
                            <div>
                                <InputField id="secret" label="Секрет" placeholder="Название секрета"
                                    v-model="formData.secret" />
                                <p v-if="errors.secret" class="text-red-600 text-sm mt-1">{{ errors.secret }}</p>
                            </div>
                            <div>
                                <InputField id="project" label="Проект" placeholder="Название проекта"
                                    v-model="formData.project" />
                                <p v-if="errors.project" class="text-red-600 text-sm mt-1">{{ errors.project }}</p>
                            </div>
                            <div>
                                <CustomSelect label="Срок доступа (TTL)" :options="ttlOptions" v-model="formData.ttl" />
                                <p v-if="errors.ttl" class="text-red-600 text-sm mt-1">{{ errors.ttl }}</p>
                            </div>
                        </div>
                        <!-- Правая колонка -->
                        <div class="flex flex-col h-full">
                            <div class="flex-grow">
                                <TextAreaField id="justification" label="Обоснование (обязательно)"
                                    placeholder="Текст обоснования" v-model="formData.justification" />
                            </div>
                            <p v-if="errors.justification" class="text-red-600 text-sm mt-1">{{ errors.justification }}
                            </p>
                        </div>
                    </div>

                    <div class="flex justify-end mt-8">
                        <BaseButton type="submit">
                            Отправить заявку
                        </BaseButton>
                    </div>
                </form>
            </div>

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['close'])


const isSubmitted = ref(false)

const ttlOptions = [
    { value: '3h', label: '3 часа (по умолчанию)' },
    { value: '1d', label: '1 день' },
    { value: 'permanent', label: 'Постоянно' }
]

const formData = ref({
    secret: 'KEYNAME',
    project: 'ИмяПроекта',
    ttl: '3h',
    justification: ''
})

const errors = ref({
    secret: '',
    project: '',
    ttl: '',
    justification: ''
})

const validateForm = () => {
    Object.keys(errors.value).forEach(key => errors.value[key] = '');
    let isValid = true;
    if (!formData.value.secret.trim()) {
        errors.value.secret = 'Поле не заполнено';
        isValid = false;
    }

    if (!formData.value.justification.trim()) {
        errors.value.justification = 'Поле не заполнено';
        isValid = false;
    }
    return isValid;
}

const submitForm = () => {
    if (!validateForm()) {
        return;
    }

    console.log('Отправка данных:', formData.value)

    isSubmitted.value = true
}
</script>
