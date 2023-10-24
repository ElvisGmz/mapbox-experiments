<template>
    <aside
        class="absolute z-50 top-0 left-0 w-full !m-0 h-[100svh] bg-white border border-gray-100 max-w-[280px] shadow-xl overflow-y-auto transition-all duration-300 ease-in-out"
        :class="{
            '-translate-x-full': !modelValue,
            'translate-x-0': modelValue,
        }"
        >
        <button class="absolute right-0 top-0 p-2 rounded-full aspect-square" type="button" @click="$emit('update:modelValue', '')">❌</button>
        <div class="divide-y divide-blue-100">
            <SideBarCollapsible />
            <SideBarCollapsible />
            <SideBarCollapsible />
        </div>
    </aside>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
import SideBarCollapsible from "./SideBarCollapsible.vue";

defineProps({
    modelValue: {
        type: String,
        default: '',
        required: true,
    }
})

defineEmits(['update:modelValue'])

</script>
