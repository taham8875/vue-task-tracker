<script setup lang="ts">
import { watchEffect, ref } from 'vue';
import { useRouter } from 'vue-router';
const currentYear = new Date().getFullYear();

const router = useRouter();

const footerLink = ref({
    name: '',
    path: ''
});

watchEffect(() => {
    if (router.currentRoute.value.path === '/') {
        footerLink.value.name = 'About';
        footerLink.value.path = '/about';
    } else {
        footerLink.value.name = 'Back to Home';
        footerLink.value.path = '/';
    }
});


</script>

<template>
    <footer class="text-center text-gray-500 text-sm mt-4">
        &copy; {{ currentYear }} Task Tracker - <router-link :to="footerLink.path" class="underline text-green-700"> {{
            footerLink.name }}</router-link>
    </footer>
</template>