<script setup>
import { defineProps, defineEmits, toRefs } from 'vue';

const emit = defineEmits(['remove']);

const props = defineProps({
  task: Object
});

const { task } = toRefs(props);

const formattedDate = (dateString) => {
  const options = { month: 'short', day: 'numeric', year: 'numeric' };
  return new Date(dateString).toLocaleDateString(undefined, options);
};

const removeTask = () => {
  emit('remove', task.value);
};
</script>

<template>
  <div class="flex items-center justify-between gap-3 w-full bg-sky-900 rounded-2xl md:px-6 md:py-5 px-3 py-2 shadow-xl">
    <div class="w-full">
      <label class="flex items-center">
        <input type="checkbox" v-model="task.done" class="hidden peer">
        <span class="flex items-center justify-center flex-shrink-0 w-5 h-5 rounded-full border-2 border-sky-600 cursor-pointer bubble shadow-md shadow-sky-600"></span>

        <div class="md:ml-6 ml-3 leading-snug text-white peer-checked:line-through">
          <p class="font-medium md:text-base text-sm">{{ task.title }}</p>
          <p class="text-xs opacity-80">{{ formattedDate(task.duedate) }}</p>
        </div>
      </label>
    </div>

    <div class="flex items-center justify-center">
      <button @click="removeTask" class="text-red-500 md:text-base text-sm hover:text-red-600 hover:drop-shadow">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="md:w-6 md:h-6 w-5 h-5">
          <path fill-rule="evenodd" d="M16.5 4.478v.227a48.816 48.816 0 013.878.512.75.75 0 11-.256 1.478l-.209-.035-1.005 13.07a3 3 0 01-2.991 2.77H8.084a3 3 0 01-2.991-2.77L4.087 6.66l-.209.035a.75.75 0 01-.256-1.478A48.567 48.567 0 017.5 4.705v-.227c0-1.564 1.213-2.9 2.816-2.951a52.662 52.662 0 013.369 0c1.603.051 2.815 1.387 2.815 2.951zm-6.136-1.452a51.196 51.196 0 013.273 0C14.39 3.05 15 3.684 15 4.478v.113a49.488 49.488 0 00-6 0v-.113c0-.794.609-1.428 1.364-1.452zm-.355 5.945a.75.75 0 10-1.5.058l.347 9a.75.75 0 101.499-.058l-.346-9zm5.48.058a.75.75 0 10-1.498-.058l-.347 9a.75.75 0 001.5.058l.345-9z" clip-rule="evenodd" />
        </svg>
      </button>
    </div>
  </div>
</template>
