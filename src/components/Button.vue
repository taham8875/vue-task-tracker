<script setup lang="ts">
import { defineProps, computed } from 'vue'

const props = defineProps({
    variant: {
        type: String,
        default: 'primary'
    }
})

const colorClasses = computed(() => {
    if (props.variant === 'primary') {
        return 'bg-black hover:bg-gray-900'
    } else if (props.variant === 'create') {
        return 'bg-green-600 hover:bg-green-700'
    } else if (props.variant === 'delete') {
        return 'bg-red-600 hover:bg-red-700'
    }
})

</script>

<template>
    <button class="btn rounded py-2 px-4 transition-colors text-white" :class="colorClasses">
        <slot></slot>
    </button>
</template>