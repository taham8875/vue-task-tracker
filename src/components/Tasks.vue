<script setup lang="ts">
import Task from './Task.vue';
import type { TasksProps } from '../../index.d';

const props = defineProps({
    tasks: {
        type: Array as () => TasksProps,
        required: true
    }
});

const emits = defineEmits(['delete-task', 'toggle-reminder']);
</script>

<template>
    <div v-for="task in tasks">
        <Task :key="task.id" :task="task" @delete-task="$emit('delete-task', task.id)"
            @toggle-reminder="$emit('toggle-reminder', task.id)" />
    </div>
</template>