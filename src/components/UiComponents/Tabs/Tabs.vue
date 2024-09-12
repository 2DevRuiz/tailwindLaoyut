<!--Nota : agregar unos botones que permita mover el scroll del contenido de la sección de tabs -->
<template>
    <div class="w-full h-full min-h-full">
        <!-- <div class="flex items-center justify-center rounded-lg p-16 dark:bg-slate-900 dark:text-white"> -->
        <div ref="tabContainer"
            class="flex h-auto w-full flex-col rounded-lg border bg-white border-slate-300 dark:border-slate-600 ">
            <!--- Mobile Section-->
            <div class="block px-2 pt-3 sm:hidden dark:text-white">
                <button @click="toggleDropdown"
                    class="relative flex w-full items-center justify-between rounded-md border border-slate-300 bg-white p-2 capitalize dark:border-slate-600 dark:bg-slate-800">
                    {{ activeTab?.title }}
                    <span class="h-5 w-5 transition-transform" :class="isDropdownOpen ? 'rotate-180' : 'rotate-0'">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 52 52"
                            enable-background="new 0 0 52 52" xml:space="preserve">
                            <path
                                d="M47.6,17.8L27.1,38.5c-0.6,0.6-1.6,0.6-2.2,0L4.4,17.8c-0.6-0.6-0.6-1.6,0-2.2l2.2-2.2  c0.6-0.6,1.6-0.6,2.2,0l16.1,16.3c0.6,0.6,1.6,0.6,2.2,0l16.1-16.2c0.6-0.6,1.6-0.6,2.2,0l2.2,2.2C48.1,16.3,48.1,17.2,47.6,17.8z" />
                        </svg>
                    </span>
                    <div v-show="isDropdownOpen"
                        class="absolute left-0 top-12 z-10 w-full rounded-md border border-slate-300 bg-white shadow-md dark:border-slate-600 dark:bg-slate-800">
                        <div v-for="(tab, index) in tabs" :key="tab" @click="setSection(index)"
                            class="cursor-pointer px-4 py-2 hover:bg-slate-200 dark:hover:bg-slate-700">
                            {{ tab.title }}
                        </div>
                    </div>
                </button>
            </div>
            <!--- Mobile Section-->

            <!--- Header Section  -->
            <div
                class="relative hidden w-full gap-4 border-b border-slate-300 px-2 sm:flex md:px-5 dark:border-slate-300 md:overflow-x-auto">
                <div class="absolute bottom-0 left-0 h-0.5  transition-transform duration-500" :style="{
                    width: underlineWidth + 'px',
                    transform: 'translateX(' + underlineOffset + 'px)',
                }" :class="[undelineClass()]">
                </div>
                <div v-for="(tab, index) in tabs" :key="index" ref="tabHeaders" @click="setSection(index)"
                    class="pb-2  pt-3 text-center md:min-w-24" :class="tabClass(index)">
                    <!-- {{ tab.charAt(0).toUpperCase() + tab.slice(1) }}-->
                    <!-- <span class=""> -->
                    {{ tab.title }}
                    <!-- </span> -->
                </div>
            </div>
            <!--- Header Section-->
            <!-- Panel Section -->
            <div class="h-full min-h-[70vh] p-0.5">
                <slot></slot>
            </div>
            <!-- Panel Section -->
        </div>
        <!-- </div> -->
    </div>

</template>
<script lang="ts" setup>
import { ref, onMounted, nextTick } from 'vue';


//variables darwing

const tabHeaders: any = ref([]);
const activeTab: any = ref(null);
//variables del codigo original 

const isDropdownOpen = ref(false)
const currentTab: any = ref(0)
const tabs: any = ref([])

const underlineWidth = ref(0);
const underlineOffset = ref(0);

//variables del codigo original de f

const tabContainer: any = ref(null);
const props = defineProps(['customClass']);

onMounted(() => {
    tabs.value = [...tabContainer.value.querySelectorAll('.tab')];
    for (let x of tabs.value) {
        if (x.classList.contains('active')) {
            currentTab.value = tabs.value.indexOf(x);
            activeTab.value = tabs.value[currentTab.value];

        }
    }
    updateUnderlinePosition();
})


//puede ser la misma que el que esta en la desktop, hay que hacer pruebas
const selectSection = (tab: any) => {
    currentTab.value = tab

    for (let x of [...tabs.value, ...tabHeaders.value]) {
        x.classList.remove('active')
    }
    tabs.value[currentTab.value].classList.add('active')
    tabHeaders.value[currentTab.value].classList.add('active')
    updateUnderlinePosition()
}
//puede ser la misma que el que esta en la mobile, hay que hacer pruebas
const setSection = (tab: any) => {
    currentTab.value = tab

    for (let x of [...tabs.value, ...tabHeaders.value]) {
        x.classList.remove('active')
    }
    tabs.value[currentTab.value].classList.add('active')
    tabHeaders.value[currentTab.value].classList.add('active')
    activeTab.value = tabs.value[currentTab.value];
    updateUnderlinePosition()
}

//oculta el dropdown par ala version de mobile 
const toggleDropdown = () => {
    isDropdownOpen.value = !isDropdownOpen.value;
}

const updateUnderlinePosition = async () => {
    let targetRef = null;
    if (tabHeaders.value[currentTab.value] === undefined) {
        await nextTick()
    }

    targetRef = tabHeaders.value[currentTab.value];
    // update for underline position
    if (targetRef) {
        underlineWidth.value = targetRef.offsetWidth;
        underlineOffset.value = targetRef.offsetLeft;

    }
};

const tabClass = (tab: any) => {
    return currentTab.value !== tab
        ? "cursor-pointer border-b border-transparent hover:border-slate-300 dark:hover:border-slate-600 hover:bg-gray-200"
        : "cursor-default text-orange-700 ";
};

const undelineClass = () => {
    return "bg-orange-500"
}

const showData = async (data: any) => {
    if (activeTab.value === null) {
        await nextTick()
    }
    console.log(activeTab.value)
    return activeTab.value?.title
}
</script>