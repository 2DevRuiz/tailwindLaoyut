<template>
    <div class="w-full h-full px-2">
        <div class="mb-5">
            <label class="text-dark mb-3 block text-base font-medium"> {{ label }} </label>
            <div class="relative">

                <label class="relative inline-flex cursor-pointer items-center">
                    <input class="peer sr-only" v-model="model" type="checkbox" />
                    <!-- Fondo del interruptor con sombra -->
                    <div
                        class="peer h-10 w-20 rounded-md border border-gray-800 bg-gray-300 transition-all duration-500 shadow-[inset_2px_-2px_4px_rgba(0,0,0,0.4)]  peer-checked:bg-green-500 peer-checked:shadow-[inset_-2px_2px_4px_rgba(0,0,0,0.4)]">
                    </div>

                    <!-- Texto de OFF -->
                    <span
                        class="absolute right-3 text-xs font-medium uppercase text-white opacity-100 transition-opacity duration-500 peer-checked:opacity-0">
                        {{text_Off}} </span>

                    <!-- Texto de ON -->
                    <span
                        class="absolute right-11 text-xs font-medium uppercase text-white opacity-0 transition-opacity duration-500 peer-checked:opacity-100">
                        {{text_On}} </span>

                    <!-- Botón deslizante con sombras para crear profundidad -->
                    <span
                        class="absolute ml-1 h-8 w-4 transform rounded-full bg-white/90 shadow-lg transition-transform duration-500 peer-checked:translate-x-14 peer-checked:duration-500" />
                </label>

            </div>
        </div>
    </div>
</template>
<script lang="ts" setup>

const model = defineModel()
const props = defineProps({
    label: {
        type: String,
        default: 'Label Defaults',
        required: false
    },
    text_On: {
        type: String,
        default: 'Yes',
        required: false
    },
    text_Off: {
        type: String,
        default: 'No',
        required: false
    }
})
</script>