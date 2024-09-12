<template>
    <!-- <div class="h-full"> -->
    <div ref="tabs" class="flex h-full min-h-[70vh] w-full tab rounded-md " :class="active ? 'active' : ''">
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