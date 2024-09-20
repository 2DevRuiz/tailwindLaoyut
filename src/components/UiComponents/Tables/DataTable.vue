<template>
    <div class="container mx-auto w-full px-2">
        <!-- Search and exports -->
        <div class="my-2 flex items-center justify-between">
            <div v-if="search">
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
        <div class="border rounded-lg overflow-auto">
            <div class="relative w-full h-full overflow-auto">
                <table class="w-full caption-bottom text-sm">
                    <thead class="">
                        <tr class="sticky border-b transition-colors hover:bg-muted/50 ">
                            <th v-for="field in displayedFields"
                                class="h-12 px-4 text-left align-middle font-medium text-muted-foreground border cursor-pointer">
                                <slot :name="`header(${field.key})`" :field="field">
                                    {{ field.label }}
                                </slot>
                            </th>

                        </tr>
                    </thead>
                    <tbody>
                        <tr v-if="loading" class="border-b transition-colors hover:bg-zinc-100/50 odd:bg-gray-100">
                            <td class="p-4  align-middle border" :colspan="displayedFieldKeys.length">
                                <div class="flex justify-center items-center  min-h-[25rem]">
                                    <span class="relative flex items-center justify-center text-gray-400  mr-3">
                                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 animate-spin" fill="none"
                                            viewBox="0 0 20 20">
                                            <path fill="currentColor" fill-rule="evenodd"
                                                d="M11,16 C12.1045695,16 13,16.8954305 13,18 C13,19.1045695 12.1045695,20 11,20 C9.8954305,20 9,19.1045695 9,18 C9,16.8954305 9.8954305,16 11,16 Z M4.74123945,13 C6.12195133,13 7.24123945,14.1192881 7.24123945,15.5 C7.24123945,16.8807119 6.12195133,18 4.74123945,18 C3.36052758,18 2.24123945,16.8807119 2.24123945,15.5 C2.24123945,14.1192881 3.36052758,13 4.74123945,13 Z M16.3193286,13.5 C17.4238981,13.5 18.3193286,14.3954305 18.3193286,15.5 C18.3193286,16.6045695 17.4238981,17.5 16.3193286,17.5 C15.2147591,17.5 14.3193286,16.6045695 14.3193286,15.5 C14.3193286,14.3954305 15.2147591,13.5 16.3193286,13.5 Z M18.5,9.31854099 C19.3284271,9.31854099 20,9.99011387 20,10.818541 C20,11.6469681 19.3284271,12.318541 18.5,12.318541 C17.6715729,12.318541 17,11.6469681 17,10.818541 C17,9.99011387 17.6715729,9.31854099 18.5,9.31854099 Z M2.5,6 C3.88071187,6 5,7.11928813 5,8.5 C5,9.88071187 3.88071187,11 2.5,11 C1.11928813,11 0,9.88071187 0,8.5 C0,7.11928813 1.11928813,6 2.5,6 Z M17.7857894,5.20724734 C18.3380741,5.20724734 18.7857894,5.65496259 18.7857894,6.20724734 C18.7857894,6.75953209 18.3380741,7.20724734 17.7857894,7.20724734 C17.2335046,7.20724734 16.7857894,6.75953209 16.7857894,6.20724734 C16.7857894,5.65496259 17.2335046,5.20724734 17.7857894,5.20724734 Z M8,0 C9.65685425,0 11,1.34314575 11,3 C11,4.65685425 9.65685425,6 8,6 C6.34314575,6 5,4.65685425 5,3 C5,1.34314575 6.34314575,0 8,0 Z M15.5,3 C15.7761424,3 16,3.22385763 16,3.5 C16,3.77614237 15.7761424,4 15.5,4 C15.2238576,4 15,3.77614237 15,3.5 C15,3.22385763 15.2238576,3 15.5,3 Z" />
                                        </svg>
                                    </span>
                                    <span class="text-gray-400">Loading</span> <!-- traducction -->
                                </div>
                            </td>
                        </tr>
                        <template v-else-if="filteredItems.length > 0">
                            <tr v-for="(item, index) in paginatedData" :key="item.name"
                                class="border-b transition-colors hover:bg-zinc-100/50 odd:bg-gray-100">
                                <template v-for="(key, index) in displayedFieldKeys" :key="index">

                                    <Component :is="cellElement(key)" class="p-4 align-middle border">
                                        <slot :name="`cell(${key})`" :value="format(item, (key))" :item="item"
                                            :index="index" :format="(k: any) => format(item, k)">
                                            {{ format(item, (key)) }}
                                        </slot>
                                    </Component>
                                </template>
                            </tr>
                        </template>
                        <tr v-else class="border-b transition-colors hover:bg-zinc-100/50 odd:bg-gray-100">
                            <td :colspan="displayedFieldKeys.length" class="p-4 align-middle border">
                                <div class="flex items-center justify-center font-semibold min-h-[25rem]">
                                    No Data
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <!-- Table -->
        <!-- Pagination -->
        <div v-if="totalPages > 1" class="my-6 flex justify-between px-6">


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
import { computed, ref, watch } from 'vue';
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
    },
    search: {
        type: Boolean,
        required: false,
        default: true
    },
    exportButtons: {
        type: Boolean,
        required: false,
        default: true
    },
    loading: {
        type: Boolean,
        required: false,
        default: false
    },
    hover: {
        type: Boolean,
        required: false,
    },
    stripe: {
        type: Boolean,
        required: false,
    },
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
 * Variables a utilizar
 */

const itemsPerPage = ref(10);
const currentPage = ref(1);

const startIndex = computed(() => (currentPage.value - 1) * itemsPerPage.value);
const endIndex = computed(() =>
    Math.min(currentPage.value * itemsPerPage.value, filteredItems.value.length),
);

watch(itemsPerPage, (newItemsPerPage: any, oldItemsPerPage: any) => {
    if (newItemsPerPage !== oldItemsPerPage) {
        // startIndex.value = currentPage.value * newItemsPerPage;
        itemsPerPage.value = newItemsPerPage;

        if (currentPage.value >= totalPages.value) {
            currentPage.value = totalPages.value;
        }
    }
});
const paginatedData = computed(() =>
    filteredItems.value.slice(startIndex.value, endIndex.value),
);

const totalPages = computed(() =>
    Math.ceil(filteredItems.value.length / itemsPerPage.value),
);

const totalItems = computed(() => filteredItems.value.length);

const goToFirstPage = () => {
    currentPage.value = 1;
};

const goToPreviousPage = () => {
    if (currentPage.value > 1) {
        currentPage.value--;
    }
};

const goToNextPage = () => {
    if (currentPage.value < totalPages.value) {
        currentPage.value++;
    }
};

const goToLastPage = () => {
    currentPage.value = totalPages.value;
};

const pages = computed(() => {
    // Maximum Pages to show on either side of the currentPage
    const pageRange = 2;

    let startPage, endPage;

    // Show All Pages if Total Pages are Less Than 5
    if (totalPages.value <= 5) {
        startPage = 1;
        endPage = totalPages.value;
    } else {
        startPage = Math.max(currentPage.value - pageRange, 1);
        endPage = Math.min(currentPage.value + pageRange, totalPages.value);

        // Showing a Maximum of 5 pages at a time
        if (endPage - startPage + 1 < 5) {
            if (currentPage.value < totalPages.value / 2) {
                endPage = Math.max(endPage + (5 - (endPage - startPage + 1)), 5);
            } else {
                startPage = Math.min(
                    startPage - (5 - (endPage - startPage + 1)),
                    totalPages.value - 4,
                );
            }
        }
    }

    // An Array to store Page Numbers
    const pagesArray = [];
    for (let i = startPage; i <= endPage; i++) {
        pagesArray.push(i);
    }
    return pagesArray;
});

/**
 * end codigo inicial
 */





</script>