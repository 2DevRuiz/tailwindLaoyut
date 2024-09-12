<template>
    <div class="w-full h-full px-2">
        <div class="mb-5">
            <label class="text-dark mb-[10px] block text-base font-medium"> {{ label }} </label>
            <div class="relative">
                <!-- <label class="relative inline-flex cursor-pointer items-center">
                    <input class="peer sr-only" value="" type="checkbox" />
                    <div
                        class="peer h-10 w-20 rounded-xl bg-gray-300 outline-none duration-100 after:absolute after:left-1 after:top-1 after:flex after:h-8 after:w-8 after:items-center after:justify-center after:rounded-full after:bg-white after:text-xs after:font-bold after:text-sky-800 after:outline-none after:duration-500 after:content-['No'] peer-checked:bg-green-300 peer-checked:after:translate-x-10 peer-checked:after:border-white peer-checked:after:content-['Yes'] peer-focus:outline-none">
                    </div>
                </label> -->
                <label class="relative inline-flex items-center cursor-pointer">
                    <input class="sr-only peer" value="" type="checkbox">
                    <div
                        class="peer rounded-lg outline-none duration-100 after:duration-500 w-28 h-12 bg-gray-300 hover:bg-gray-400 peer-focus:outline-none 
                           after:absolute after:outline-none after:rounded-full after:h-10 after:w-10 after:bg-white after:top-1 
                        after:left-1 after:flex after:justify-center after:items-center 
                         after:text-sky-800 after:font-bold peer-checked:bg-green-700 peer-checked:hover:bg-green-400 peer-checked:after:translate-x-16  peer-checked:after:border-white">
                    </div>
                </label>
            </div>
        </div>
    </div>
</template>
<script lang="ts" setup>

const props = defineProps({
    label: {
        type: String,
        default: 'Label Defaults',
        required: false
    }
})
</script>