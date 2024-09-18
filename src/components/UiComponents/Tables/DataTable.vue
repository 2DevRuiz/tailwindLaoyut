<template>
    <div class="container mx-auto w-full px-2">
        <!-- Search and exports -->
        <div class="my-2 flex items-center justify-between">
            <div>
                <input type="text" placeholder="Search..." v-model="searchValue"
                    class="rounded-lg border-0 p-1.5 px-3 py-2 shdow-sm ring-1 ring-slate-300 placeholder:text-slate-400 focus:outline-none lg:w-96 dark:bg-slate-200" />
            </div>
            <div class="flex gap-2">
                <button
                    class="flex justify-center gap-2 rounded-lg bg-green-500 px-2 py-2 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-green-600 focus:outline-none sm:px-4">
                    <p class="hidden md:block">Download Excel</p>
                </button>
                <button
                    class="flex justify-center gap-2 rounded-lg bg-red-500 px-2 py-2 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-red-600 focus:outline-none sm:px-4">
                    <p class="hidden md:block">Download PDF</p>
                </button>
            </div>
        </div>
        <!-- Search and exports -->
        <!-- Table -->
        <div class="container max-h-96 overflow-y-auto ">
            <table class="w-full overflow-auto">
                <!-- thead -->
                <thead>
                    <tr class="sticky top-0 z-10 bg-cyan-100 text-left ">
                        <th v-for="field in displayedFields" class="cursor-pointer text-nowrap p-4 border">
                            <div class="flex items-center">
                                <slot :name="`header(${field.key})`" :field="field">
                                    {{ field.label }}
                                </slot>
                            </div>
                        </th>
                    </tr>
                </thead>
                <!-- thead   -->
                <!-- tbody -->
                <tbody>
                    <tr v-for="(item, index) in filteredItems" :key="item.name">

                        <template v-for="key in displayedFieldKeys">

                            <Component :is="cellElement(key)" class="p-4 border">
                                <slot :name="`cell(${key})`" :value="format(item, (key))" :item="item" :index="index"
                                    :format="(k: any) => format(item, k)">
                                    {{ format(item, (key)) }}
                                </slot>
                            </Component>

                        </template>

                    </tr>
                </tbody>
                <!-- tbody -->
            </table>
        </div>
        <!-- Table -->
        <!-- Pagination -->
        <div v-if="totalPages > 1" class="mt-4 grid grid-cols-3 px-6">
            <div></div>

            <div class="flex scale-75 items-center justify-center gap-4 sm:scale-100">
                <button @click="goToFirstPage" :disabled="currentPage === 1"
                    class="rounded-full focus:outline-none focus:ring-2 focus:ring-cyan-500" :class="currentPage === 1
                        ? 'disabled: cursor-auto'
                        : 'hover:bg-cyan-100 dark:hover:bg-cyan-500'
                        ">
                    << <!-- <ChevronDoubleLeftIcon class="size-9 rounded-full p-2" /> -->
                </button>
                <button @click="goToPreviousPage" :disabled="currentPage === 1"
                    class="rounded-full focus:outline-none focus:ring-2 focus:ring-cyan-500" :class="currentPage === 1
                        ? 'disabled: cursor-auto'
                        : 'hover:bg-cyan-100 dark:hover:bg-cyan-500'
                        ">
                    < <!-- <ChevronLeftIcon class="size-9 rounded-full p-2" /> -->
                </button>
                <button v-for="page in pages" :key="page" @click="currentPage = page"
                    class="flex size-9 items-center justify-center rounded-full p-2 hover:bg-cyan-100 focus:outline-none focus:ring-2 focus:ring-cyan-500 dark:hover:bg-cyan-500"
                    :class="{
                        'rounded-none border-b-2 border-cyan-500 font-semibold text-cyan-500 hover:bg-transparent dark:hover:bg-transparent':
                            page === currentPage,
                    }">
                    {{ page }}
                </button>
                <button @click="goToNextPage" :disabled="currentPage === totalPages"
                    class="rounded-full focus:outline-none focus:ring-2 focus:ring-cyan-500" :class="currentPage === totalPages
                        ? 'disabled: cursor-auto'
                        : 'hover:bg-cyan-100 dark:hover:bg-cyan-500'
                        ">
                    >
                    <!-- <ChevronRightIcon class="size-9 rounded-full p-2" /> -->
                </button>
                <button @click="goToLastPage" :disabled="currentPage === totalPages"
                    class="rounded-full focus:outline-none focus:ring-2 focus:ring-cyan-500" :class="currentPage === totalPages
                        ? 'disabled: cursor-auto'
                        : 'hover:bg-cyan-100 dark:hover:bg-cyan-500'
                        ">
                    >>
                    <!-- <ChevronDoubleRightIcon class="size-9 rounded-full p-2" /> -->
                </button>
            </div>

            <div class="hidden items-center justify-end gap-4 xl:flex">
                <label for="items-per-page">Items per page:
                    <select v-model="itemsPerPage"
                        class="ml-2 rounded-lg bg-cyan-100 p-1 focus:outline-none focus:ring-2 focus:ring-cyan-500 dark:bg-cyan-500">
                        <option value="5">5</option>
                        <option value="10">10</option>
                        <option value="15">15</option>
                    </select></label>
                <span>
                    {{ (currentPage - 1) * itemsPerPage + 1 }}
                    -
                    {{ Math.min(currentPage * itemsPerPage, totalItems) }}
                    of
                    {{ totalItems }} items
                </span>
            </div>
        </div>
        <!-- Pagination -->
    </div>
</template>
<script lang="ts" setup>
import { computed, ref } from 'vue';
interface fieldsProps {
    label: string
    key: string
    ordered: boolean
    hidden?: boolean
    header?: boolean
    format?: (value: any) => any
}
// Props
const props = defineProps({
    fields: {
        type: Array<fieldsProps>,
        required: true,
        default: () => []
    },
    items: {
        type: Array<any>,
        required: false,
        default: () => []
    }
})
/**
 * Variable declaration
 */
// Search Value For Filtering
const searchValue = ref('');

// Vizualization de campos
const displayedFields = computed(() => props.fields.filter((i) => !i.hidden))
const displayedFieldKeys = computed(() => {
    const obj = Object.entries(displayedFields.value).map(([_key, value]) => value.key);
    return obj
})


/**
 * Codigo Inicial
 */
const currentSort = ref({
    column: 'key', //change to initialSortField
    typeSorting: 'asc'
})

const cellElement = (key: string) => {
    const field = props.fields.find((f) => f.key === key)
    return field && field.header ? 'th' : 'td'
}

const format = (item: any, key: any) => {
    const field = props.fields.find((f) => f.key === key)
    console.log(item[key])
    return field && field.format ? field.format(item[key]) : item[key]
}
const compareData = (a: any, b: any, columnName: any) => {
    const valueA = a[columnName];
    const valueB = b[columnName];

    if (typeof valueA === 'string') {
        return currentSort.value.typeSorting === 'asc' ? valueA.localeCompare(valueB) : valueB.localeCompare(valueA);
    } else {
        return currentSort.value.typeSorting === 'asc' ? valueA - valueB : valueB - valueA;
    }
}

const filteredItems: any = computed(() => {
    const keys = displayedFieldKeys.value;
    if (searchValue.value !== '') {

        const filteredArray = props.items.filter((item) => {
            for (let i = 0; i < keys.length; i++) {
                const key = keys[i];
                if (item[key] !== undefined && typeof item[key] === 'string') {
                    if (item[key] && item[key].toLocaleLowerCase().includes(searchValue.value.toLocaleLowerCase())) {
                        return true;
                    }
                } else if (typeof item[key] === 'number') {
                    if (item[key] && item[key].toString().includes(searchValue.value.toLocaleLowerCase())) {
                        return true;
                    }
                }
            }
            return false;
        });
        return filteredArray.sort((a, b) => compareData(a, b, currentSort.value.column));
    }
    return props.items.sort((a, b) => compareData(a, b, currentSort.value.column));
});




/**
 * end codigo inicial
 */
const totalPages = 5;
const totalItems = 100;
const itemsPerPage = 10;
const currentPage = ref(1);
const pages = Array.from({ length: totalPages }, (_, i) => i + 1);


const goToFirstPage = () => {

}
const goToPreviousPage = () => {

}
const goToNextPage = () => {

}
const goToLastPage = () => {

}
console.log(props.fields)

</script>