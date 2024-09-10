<template>
    <div class="w-full h-full">
        <div class="w-full px-4">
            <div class="mb-12">
                <label class="text-dark mb-[10px] block text-base font-medium"> {{ label }} </label>
                <div class="relative">
                    <input type="email" placeholder="Devid Jhon" v-model="model"
                        class="text-dark-6 w-full rounded-md border border-gray-700 placeholder-gray-500 bg-transparent py-[10px] pl-5 pr-12 outline-none transition"
                        :class="{ 'border-red-500': error }" />
                    <span v-if="error" class="absolute right-4 top-1/2 -translate-y-1/2">
                        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M9.9987 2.50065C5.85656 2.50065 2.4987 5.85852 2.4987 10.0007C2.4987 14.1428 5.85656 17.5007 9.9987 17.5007C14.1408 17.5007 17.4987 14.1428 17.4987 10.0007C17.4987 5.85852 14.1408 2.50065 9.9987 2.50065ZM0.832031 10.0007C0.832031 4.93804 4.93609 0.833984 9.9987 0.833984C15.0613 0.833984 19.1654 4.93804 19.1654 10.0007C19.1654 15.0633 15.0613 19.1673 9.9987 19.1673C4.93609 19.1673 0.832031 15.0633 0.832031 10.0007Z"
                                fill="#DC3545" />
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M10.0013 5.83398C10.4615 5.83398 10.8346 6.20708 10.8346 6.66732V10.0007C10.8346 10.4609 10.4615 10.834 10.0013 10.834C9.54106 10.834 9.16797 10.4609 9.16797 10.0007V6.66732C9.16797 6.20708 9.54106 5.83398 10.0013 5.83398Z"
                                fill="#DC3545" />
                            <path fill-rule="evenodd" clip-rule="evenodd"
                                d="M9.16797 13.3333C9.16797 12.8731 9.54106 12.5 10.0013 12.5H10.0096C10.4699 12.5 10.843 12.8731 10.843 13.3333C10.843 13.7936 10.4699 14.1667 10.0096 14.1667H10.0013C9.54106 14.1667 9.16797 13.7936 9.16797 13.3333Z"
                                fill="#DC3545" />
                        </svg>
                    </span>
                </div>
                <p v-show="error" class="text-red-500 mt-[10px] text-sm">{{ errorMessage }}</p>
            </div>
        </div>
    </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import type { InputHTMLAttributes } from "vue";
// import { errorMessages } from "vue/compiler-sfc";
type InputTypes = Extract<
    InputHTMLAttributes["type"],
    "text" | "number" | "email" | "password" | "tel" | "url"
>;
interface InputProps {
    label?: string;
    type?: InputTypes;
    placeholder?: string;
    disabled?: boolean;
    readonly?: boolean;
    clearable?: boolean;
    errorMessage?: string;
    error?: boolean;
    prependIcon?: string;
    appendIcon?: string;
}
const model = defineModel()
const props = defineProps({
    error: {
        type: Boolean,
        default: false,
        required: false
    },
    placeholder: {
        type: String,
        default: '',
        required: false
    },
    label: {
        type: String,
        default: 'Default Text',
        required: false
    },
    errorMessage: {
        type: String,
        default: '',
        required: false
    }
})

const msg = ref('Hello World!')
</script>