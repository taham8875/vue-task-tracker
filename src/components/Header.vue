<script setup lang="ts">
import Button from './Button.vue';
import { computed } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const showAddTaskButton = computed(() => {
    if (router.currentRoute.value.path === '/') {
        return true;
    } else {
        return false;
    }
});

const props = defineProps({
    showAddTaskForm: {
        type: Boolean,
        required: true
    }
});

const buttonVariant = computed(() => {
    if (props.showAddTaskForm) {
        return 'delete';
    } else {
        return 'create';
    }
});

const buttonLabel = computed(() => {
    if (props.showAddTaskForm) {
        return 'Close';
    } else {
        return 'Create Task';
    }
});
</script>

<template>
    <header class="flex justify-between items-center">
        <h1 class="text-2xl">Task Tracker</h1>
        <Button v-show="showAddTaskButton" @click="$emit('toggle-add-task-form')" :variant="buttonVariant">{{ buttonLabel
        }}</Button>
    </header>
</template>