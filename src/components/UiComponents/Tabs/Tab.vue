<template>
    <!-- <div class="h-full"> -->
    <div ref="tabs" :tab_title="tab_title" class="flex h-full min-h-[70vh] w-full tab rounded-md "
        :class="active ? 'active' : ''">
        <slot></slot>
    </div>
    <!-- </div> -->
</template>
<script lang="ts" setup>
import { ref } from 'vue'

const props = defineProps({
    active: {
        type: Boolean,
        default: false,
        required: false
    },
    tab_title: {
        type: String,
        default: '',
        required: false
    }
})
</script>

<style scoped>
.tab {
    @apply hidden;
}

.tab.active {
    @apply flex;
}
</style>