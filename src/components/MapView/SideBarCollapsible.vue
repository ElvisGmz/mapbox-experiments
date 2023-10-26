<template>
    <details>
        <summary class="list-none cursor-pointer p-4">
            {{ name }}
        </summary>

        <ul class="bg-blue-50 px-4 py-4">
            <li>
                Item 1
            </li>
            <li>
                Item 2
            </li>
            <li>
                Item 3
            </li>
        </ul>
    </details>
</template>

<script setup>
import { defineProps } from 'vue';

defineProps({
    name: {
        type: String,
        default: '',
        required: true
    }
})
</script>

<style scoped>
details summary::-webkit-details-marker {
    display: none;
}
</style>