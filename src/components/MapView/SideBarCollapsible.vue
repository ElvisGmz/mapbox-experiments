<template>
     <button @click="$emit('select', data)" class="list-none cursor-pointer p-4 block w-full text-left">
        {{ data?.name }} {{ data?.last_name }}
        </button>
</template>

<script setup>
import { defineProps } from 'vue';

defineProps({
    data: {
        type: Object,
        default: () => {},
        required: true
    }
})
</script>

<style scoped>
details summary::-webkit-details-marker {
    display: none;
}
</style>