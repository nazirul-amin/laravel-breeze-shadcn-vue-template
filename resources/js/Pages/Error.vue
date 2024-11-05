<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({ status: Number })

const title = computed(() => {
    return {
        503: '503: Service Unavailable',
        500: '500: Server Error',
        404: '404: Page Not Found',
        403: '403: Forbidden',
    }[props.status] || 'Error'
})

const description = computed(() => {
    return {
        503: 'Sorry, we are doing some maintenance. Please check back soon.',
        500: 'Whoops, something went wrong on our servers.',
        404: 'Sorry, the page you are looking for could not be found.',
        403: 'Sorry, you are forbidden from accessing this page.',
    }[props.status] || 'An unexpected error occurred.'
})
</script>

<template>
    <div class="flex items-center justify-center h-screen text-center bg-gray-100">
        <div class="max-w-lg p-8 bg-white rounded-lg shadow-md">
            <h1 class="mb-4 text-4xl font-bold text-gray-800">{{ title }}</h1>
            <p class="mb-6 text-lg text-gray-600">{{ description }}</p>
            <Link
                href="/"
                class="inline-block px-6 py-2 text-white transition duration-200 bg-blue-500 rounded-lg hover:bg-blue-600"
            >
                Go Back to Home
            </Link>
        </div>
    </div>
</template>
