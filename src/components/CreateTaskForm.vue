<script setup lang="ts">
import Button from './Button.vue';
import { ref, watchEffect } from 'vue';

const taskDetails = ref({
    name: '',
    day: '',
    reminder: false
});

const emit = defineEmits(['create-new-task']);

const errorMessage = ref<string>('');

function emitCreateNewTask() {
    if (taskDetails.value.name === '' || taskDetails.value.day === '') {
        errorMessage.value = 'Please fill out all fields';
        return;
    }
    emit('create-new-task', taskDetails.value);
}



watchEffect(() => {
    if (taskDetails.value.name !== '' || taskDetails.value.day !== '') {
        errorMessage.value = '';
    }
});
</script>

<template>
    <form @submit.prevent="emitCreateNewTask" class="flex flex-col gap-4">

        <label class="flex flex-col">Task Name
            <input class="border border-gray-200 p-2 rounded" type="text" id="task-name" v-model="taskDetails.name" />
        </label>

        <label class="flex flex-col relative">Date
            <input class="border border-gray-200 p-2 rounded" type="date" id="task-day" v-model="taskDetails.day" />
        </label>

        <label class="flex items-center gap-40">Set Reminder
            <input type="checkbox" id="task-reminder" v-model="taskDetails.reminder" />
        </label>

        <p class="text-red-500">{{ errorMessage }}</p>

        <Button type="submit" class="w-full">Create Task</Button>
    </form>
</template>

<style scoped>
@tailwind base;
@tailwind components;
@tailwind utilities;

/* to activate the calendar on focus of the input element. Not only on the icon of the calender */
input[type="date"]::-webkit-calendar-picker-indicator {
    @apply bg-transparent bottom-0 opacity-0 cursor-pointer h-auto left-0 absolute right-0 top-0 w-auto;
}
</style>