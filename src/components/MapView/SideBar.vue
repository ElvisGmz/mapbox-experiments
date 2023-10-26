<template>
    <aside
        class="absolute z-50 top-0 left-0 w-full !m-0 h-[100svh] bg-white border border-gray-100 max-w-[280px] shadow-xl overflow-y-auto transition-all duration-300 ease-in-out"
        :class="{
            '-translate-x-full': !modelValue,
            'translate-x-0': modelValue,
        }"
        >
        <button class="absolute right-0 top-0 p-2 rounded-full aspect-square" type="button" @click="$emit('update:modelValue', null)">❌</button>
        <div class="divide-y divide-blue-100">

            <input type="text" placeholder="Search" v-model="query" class="px-4 py-2.5 w-full" />

            <SideBarCollapsible v-for="(item, index) in filterItems" :name="`${item.name} ${item.last_name}`" :key="index" />
        </div>
    </aside>
</template>

<script setup>
import { defineProps, defineEmits, ref, computed } from 'vue'
import SideBarCollapsible from "./SideBarCollapsible.vue";

const props = defineProps({
    modelValue: {
        type: Array || null, 
        default: () => null,
        required: true,
    }
})

const query = ref('')

const filterItems = computed(() => {
    const results = (props.modelValue || [])?.filter((item) => {
      const fullName = `${item?.name} ${item?.last_name}`.toLowerCase();
      const result = fullName.search(query.value.toLowerCase());

      return result >= 0;
    });
    return results || []
})

defineEmits(['update:modelValue'])

</script>
