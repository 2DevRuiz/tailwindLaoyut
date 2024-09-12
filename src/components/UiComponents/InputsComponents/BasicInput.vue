<template>
    <div class="w-full h-full px-2">
        <!-- <div class="w-full px-4"> -->
        <div class="mb-5">
            <label class="text-dark mb-[10px] block text-base font-medium"> {{ label }} </label>
            <div class="relative">
                <!-- <input :type="type" :placeholder="placeholder" v-model="model"
                        class="text-dark-6 w-full rounded-md border border-gray-700 placeholder-gray-500 bg-transparent py-[10px] pl-5 pr-12 outline-none transition"
                        :class="{ 'border-red-500': error }" /> -->
                <div class="flex items-center border-0 border-gray-300 rounded-md shadow-sm p-0.5">

                    <input :type="type" v-model="model"
                        class="text-dark-6 w-full rounded-md  border border-r-none  border-gray-700 placeholder-gray-500 bg-transparent py-[10px] pl-5 pr-4 lg:pr-5 outline-none transition"
                        :placeholder="placeholder" :class="{
                            'border-red-500': error,
                            'rounded-r-none border-r-0': actionButtonSlot,
                            'rounded-r-md border-r': !actionButtonSlot,
                            'border-r-gray-700': !error && !actionButtonSlot,
                            'border-r-red-500': error,
                        }" />
                    <div v-if="actionButtonSlot"
                        class=" rounded-r-md border border-l-0 border-gray-700 bg-emerald-300  h-[2.9rem] w-16 flex  overflow-hidden"
                        :class="{ 'border-l-0 border border-red-500': error }">
                        <div class="h-full w-full bg-green-700 ">
                            <slot name="InputButton">
                                <div
                                    class="h-full w-full bg-gray-100 hover:bg-gray-200 flex items-center justify-center">
                                    <!-- cambiar el icono a fontawesome -->
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-500"
                                        viewBox="0 0 20 20" fill="currentColor">
                                        <path
                                            d="M10 3.5C6.673 3.5 4.007 5.79 3 8c1.007 2.21 3.673 4.5 7 4.5s5.993-2.29 7-4.5c-1.007-2.21-3.673-4.5-7-4.5zM10 2a9.67 9.67 0 017.5 4.5c-1.43 2.36-4.18 4.5-7.5 4.5S3.93 8.86 2.5 6.5A9.67 9.67 0 0110 2zm0 7a2.5 2.5 0 100-5 2.5 2.5 0 000 5z" />
                                    </svg>
                                </div>

                            </slot>

                        </div>

                    </div>
                </div>
                <span v-if="error" class="absolute  top-1/2 -translate-y-1/2"
                    :class="{ 'right-4': !actionButtonSlot, 'right-16': actionButtonSlot }">
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
            <p v-show="error" class="absolute text-red-500 mt-2 text-sm min-h-[1rem]">{{ errorMessage }}</p>
        </div>
        <!-- </div> -->
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
    actionButtonSlot?: boolean;
}
const props = defineProps<InputProps>()

const model = defineModel()
const msg = ref('Hello World!')
</script>