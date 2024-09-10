<template>
    <div class="flex items-center justify-center bg-white p-16 text-slate-800 dark:bg-slate-900 dark:text-slate-100">
        <div class="flex h-96 w-full flex-col rounded-lg border border-slate-300 dark:border-slate-600">
            <div class="block px-2 pt-3 sm:hidden">
                <button @click="toggleDropdown"
                    class="relative flex w-full items-center justify-between rounded-md border border-slate-300 bg-white p-2 capitalize dark:border-slate-600 dark:bg-slate-800">
                    {{ currentSection }}
                    <span class="h-5 w-5 transition-transform"
                        :class="isDropdownOpen ? 'rotate-180' : 'rotate-0'">V</span>
                    <div v-show="isDropdownOpen"
                        class="absolute left-0 top-12 z-10 w-full rounded-md border border-slate-300 bg-white shadow-md dark:border-slate-600 dark:bg-slate-800">
                        <slot name="dropdown"></slot>
                    </div>
                </button>
            </div>

            <div
                class="relative hidden w-full gap-4 border-b border-slate-300 px-2 pt-3 sm:flex md:px-5 dark:border-slate-600">
                <div class="absolute bottom-0 left-0 h-0.5 bg-indigo-500 transition-transform duration-500" :style="{
                    width: underlineWidth + 'px',
                    transform: 'translateX(' + underlineOffset + 'px)',
                }"></div>
                <slot name="tabs"></slot>
            </div>

            <div class="h-full">
                <slot :current-section="currentSection"></slot>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const currentSection = ref('');
const isDropdownOpen = ref(false);

const underlineWidth = ref(0);
const underlineOffset = ref(0);

const toggleDropdown = () => {
    isDropdownOpen.value = !isDropdownOpen.value;
};

const selectSection = (section) => {
    currentSection.value = section;
    updateUnderlinePosition(section);
};

const setSection = (section) => {
    currentSection.value = section;
    updateUnderlinePosition(section);
};

const updateUnderlinePosition = (section) => {
    // You'll need to implement this based on how you want to manage tab position
};

onMounted(() => {
    // Initialize with default section
});
</script>
