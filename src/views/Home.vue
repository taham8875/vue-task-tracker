<script setup lang="ts">
import CreateTaskForm from '../components/CreateTaskForm.vue';

import { ref, onMounted } from 'vue';

import Tasks from '../components/Tasks.vue';

import type { TasksProps } from '../../index.d';

const props = defineProps({
    showAddTaskForm: {
        type: Boolean,
        required: true
    }
});

type TaskDetailsProps = {
    name: string,
    day: string,
    reminder: boolean
}


const tasks = ref<TasksProps>([]);


onMounted(async () => {
    const res = await fetch('/api/tasks');
    tasks.value = await res.json();
});

const createNewTask = async (taskDetails: TaskDetailsProps) => {
    const res = await fetch('/api/tasks', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            text: taskDetails.name,
            day: taskDetails.day,
            reminder: taskDetails.reminder
        })
    });

    const data = await res.json();

    tasks.value.push(data);
}

const deleteTask = async (id: number) => {
    await fetch(`/api/tasks/${id}`, {
        method: 'DELETE'
    });

    const res = await fetch('/api/tasks');

    if (!res.ok) {
        throw new Error('Something went wrong');
    }

    tasks.value = tasks.value.filter((task) => task.id !== id);
}

const toggleReminder = async (id: number) => {
    const taskToToggle = tasks.value.find((task) => task.id === id);

    if (!taskToToggle) {
        throw new Error('Something went wrong');
    }

    const res = await fetch(`/api/tasks/${id}`, {
        method: 'PATCH',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            reminder: !taskToToggle.reminder
        })
    });

    const data = await res.json();

    tasks.value = tasks.value.map((task) => {
        if (task.id === id) {
            return { ...task, reminder: data.reminder };
        } else {
            return task;
        }
    });
}

</script>

<template>
    <CreateTaskForm v-if="showAddTaskForm" @create-new-task="createNewTask" />
    <Tasks :tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder" />
</template>