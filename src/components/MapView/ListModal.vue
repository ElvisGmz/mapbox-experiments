<template>
  <Transition
    enter-from-class="opacity-0"
    enter-active-class="transition-opacity duration-300 ease-in-out"
    enter-to-class="opacity-100"
    leave-from-class="opacity-100"
    leave-active-class="transition-opacity duration-300 ease-in-out"
    leave-to-class="opacity-0"
  >
    <div
      v-if="data && Object.keys(data).length > 0"
      class="absolute !m-0 z-50 inset-0 bg-gray-900/40 overflow-y-auto h-full p-4 flex items-center justify-center"
      @click="$emit('close')"
    >
      <div
        class="bg-white rounded-[16px] w-full max-w-[284px] relative flex flex-col max-h-full overflow-y-auto"
        @click.stop=""
      >
        <div
          class="flex gap-4 justify-between sticky top-0 left-0 w-full bg-white p-4"
        >
          <div class="flex gap-4">
            <img
              class="object-cover aspect-square rounded-[12px] w-[48px] bg-[#F2F2F2]"
              src="https://images.unsplash.com/photo-1438761681033-6461ffad8d80?auto=format&fit=crop&q=80&w=1000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8cGVyc29ufGVufDB8fDB8fHww"
              alt="Person Avatar"
            />
            <img
              class="object-contain aspect-square rounded-[12px] w-[48px] bg-[#F2F2F2] p-[3px]"
              src="https://logodownload.org/wp-content/uploads/2021/09/star-plus-logo.png"
              alt=""
            />
          </div>
          <button
            class="p-2 rounded-full aspect-square absolute top-0 right-0 group"
            type="button"
            @click="
              $emit('close'),
                (showAllDescription = false),
                (isSocialsListOpen = false)
            "
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

        <div class="space-y-2 font-sans text-base px-4 py-2">
          <p class="text-[#0A314C] font-semibold">
            {{ data?.name }} {{ data?.last_name }}
          </p>
          <p
            class="text-sm text-[#6D6D6D]"
            :class="{
              'line-clamp-3': !showAllDescription,
            }"
          >
            {{ data?.description }}
          </p>
          <button
            v-if="!showAllDescription"
            type="button"
            class="text-sm text-[#B6044F] font-semibold"
            @click="showAllDescription = true"
          >
            Ver más
          </button>

          <div>
            <button
              type="button"
              class="text-sm text-[#6D6D6D] py-2 flex justify-between gap-6 w-full"
              @click="isSocialsListOpen = !isSocialsListOpen"
            >
              <span>Sociales</span>

              <svg
                :class="{
                  'rotate-180': isSocialsListOpen,
                }"
                xmlns="http://www.w3.org/2000/svg"
                width="20"
                height="20"
                viewBox="0 0 20 20"
                fill="none"
              >
                <path
                  d="M14.0834 7.6665C13.75 7.33317 13.25 7.33317 12.9167 7.6665L10 10.5832L7.08335 7.6665C6.75002 7.33317 6.25002 7.33317 5.91669 7.6665C5.58335 7.99984 5.58335 8.49984 5.91669 8.83317L9.41669 12.3332C9.58335 12.4998 9.75002 12.5832 10 12.5832C10.25 12.5832 10.4167 12.4998 10.5834 12.3332L14.0834 8.83317C14.4167 8.49984 14.4167 7.99984 14.0834 7.6665Z"
                  fill="#121212"
                />
              </svg>
            </button>

            <Transition
              enter-from-class="opacity-0"
              enter-active-class="transition-opacity duration-300 ease-in-out"
              enter-to-class="opacity-100"
              leave-from-class="opacity-100"
              leave-active-class="transition-opacity duration-300 ease-in-out"
              leave-to-class="opacity-0"
            >
              <div v-if="isSocialsListOpen">
                <ul class="text-sm border-l-4 pl-2">
                  <li
                    class="py-1"
                    v-for="social in data?.socials"
                    :key="social.link"
                  >
                    <a
                      :href="social.link"
                      target="_blank"
                      rel="noopener noreferrer"
                    >
                      {{ social.platform }}
                    </a>
                  </li>
                </ul>
              </div>
            </Transition>
          </div>
        </div>

        <div class="flex items-center gap-2 p-4">
          <a
            href="#"
            class="text-xs text-[#121212] px-2 py-1 rounded-[100px] bg-[#F3CD48]"
          >
            Categoria
          </a>
          <a
            href="#"
            class="text-xs text-white px-2 py-1 rounded-[100px] bg-[#BF2E27]"
          >
            Negocio
          </a>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { defineProps, defineEmits, ref } from "vue";

const isSocialsListOpen = ref(true);
const showAllDescription = ref(false);

defineEmits(["close"]);

defineProps({
  data: {
    type: Object || null,
    default: null,
    required: true,
  },
});
</script>
