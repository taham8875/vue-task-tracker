<script setup lang="ts">
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import { ref } from 'vue';

const showAddTaskForm = ref(false);

const toggleAddTaskForm = () => {
    showAddTaskForm.value = !showAddTaskForm.value;
}
</script>

<template>
    <Header @toggle-add-task-form="toggleAddTaskForm" :showAddTaskForm="showAddTaskForm" />
    <router-view :showAddTaskForm="showAddTaskForm"></router-view>
    <Footer />
</template>


<style>
#app {
    @apply max-w-xl mx-auto my-3 px-8 py-5 border border-gray-200 rounded;
}
</style>