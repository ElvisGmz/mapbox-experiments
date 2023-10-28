<template>
  <aside
    class="absolute z-40 top-0 left-0 w-full !m-0 h-[100svh] bg-white border border-gray-100 max-w-[280px] shadow-xl overflow-y-auto transition-all duration-300 ease-in-out"
    :class="{
      '-translate-x-full': !modelValue,
      'translate-x-0': modelValue,
    }"
  >
    <div
      class="sticky top-0 left-0 w-full flex justify-between bg-white border-b"
    >
      <input
        type="text"
        placeholder="Search"
        v-model="query"
        class="px-4 py-2.5 w-full"
      />
      <button
        class="p-2 rounded-full aspect-square sticky top-0 right-0 group"
        type="button"
        @click="$emit('update:modelValue', null)"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          class="w-6 h-6 stroke-[#121212] group-hover:stroke-[#808080] transition-colors duration-300 ease-in-out"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>
    </div>

    <div class="divide-y divide-blue-100">
      <SideBarCollapsible
        v-for="(item, index) in filterItems"
        :data="item"
        :key="index"
        @select="selectPerson"
      />
    </div>
  </aside>

  <ListModal :data="selectedPerson" @close="selectedPerson = null" />
</template>

<script setup>
import { defineProps, defineEmits, ref, computed } from "vue";
import SideBarCollapsible from "./SideBarCollapsible.vue";
import ListModal from "./ListModal.vue";

const props = defineProps({
  modelValue: {
    type: Array || null,
    default: () => null,
    required: true,
  },
});

const query = ref("");

const filterItems = computed(() => {
  const results = (props.modelValue || [])?.filter((item) => {
    const fullName = `${item?.name} ${item?.last_name}`.toLowerCase();
    const result = fullName.search(query.value.toLowerCase());

    return result >= 0;
  });
  return results || [];
});

defineEmits(["update:modelValue"]);

const selectedPerson = ref(null);

function selectPerson(person) {
  selectedPerson.value = person;
}
</script>
