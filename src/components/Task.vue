<script setup lang="ts">
import type { TaskProps } from '../../index.d';
import CancelIcon from './CancelIcon.vue';

const props = defineProps({
    task: {
        type: Object as () => TaskProps,
        required: true
    }
});

const emits = defineEmits(['delete-task', 'toggle-reminder']);

</script>

<template>
    <div class="flex items-center justify-between bg-gray-100 rounded p-4 my-4 hover:scale-105 transition-transform"
        :class="task.reminder ? 'border-l-4 border-green-600' : ''" @dblclick="$emit('toggle-reminder', task.id)">
        <div>
            <h3 class="text-xl font-semibold">{{ task.text }}</h3>
            <p class="text-gray-500">{{ task.day }}</p>
        </div>
        <div>
            <span @click="$emit('delete-task', task.id)"
                class="text-red-600 hover:text-red-700 transition-colors cursor-pointer">
                <CancelIcon />
            </span>
        </div>
    </div>
</template>