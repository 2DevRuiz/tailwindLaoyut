<template>
    <!-- <div class="h-full"> -->
    <div ref="tabs" class="flex h-full w-full tab" :class="active ? 'active' : ''">
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
    @apply flex h-full w-full bg-cyan-900;
}
</style>