<template>
    <select class="px-4 py-2.5 appearance-none cursor-pointer min-w-[280px]" :value="modelValue" @change="(e) => $emit('update:modelValue', e.target.value)">
        <option value="" selected>Todos</option>
        <option value="category-1">Category 1</option>
        <option value="category-2">Category 2</option>
        <option value="category-3">Category 3</option>
        <option value="category-4">Category 4</option>
        <option value="category-5">Category 5</option>
    </select>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
    modelValue: {
        type: String,
        default:'',
        required: true,
    }
})

defineEmits(['update:modelValue'])
</script>
