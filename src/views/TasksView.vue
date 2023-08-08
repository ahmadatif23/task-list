<script setup>
import { ref, computed } from 'vue';
import TaskCard from '../components/TaskCard.vue'
import Pagination from '../components/Pagination.vue'

const tasks = ref([])
const input_content = ref('')
const input_date = ref(null)
const dateInput = ref(null);

const currentPage = ref(1);
const tasksPerPage = 5;

const totalPages = computed(() => Math.ceil(tasks.value.length / tasksPerPage));
const minDate = computed(() => new Date().toISOString().split('T')[0]);

const paginatedTasks = computed(() => {
  const startIndex = (currentPage.value - 1) * tasksPerPage;
  const endIndex = startIndex + tasksPerPage;
  return tasks.value.slice(startIndex, endIndex);
});

const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

const showDatePicker = () => {
  if (dateInput.value) {
    dateInput.value.showPicker();
  }
};

const addTask = () => {
  if (input_content.value.trim() === '' || input_date.value === null ) return

  tasks.value.push({
    title: input_content.value,
    duedate: input_date.value,
    done: false
  })

  input_content.value = ''
}

const removeTask = (task) => {
  tasks.value = tasks.value.filter(t => t !== task);

  if (currentPage.value > totalPages.value) {
    if (totalPages.value !== 0) {
        currentPage.value = totalPages.value;
    }
  }
};

</script>

<template>
  <main class="w-full p-6 text-[#f7f9fd]">
    <section class="">
      <RouterLink to="/" class="hover:opacity-70 transition-all duration-100">
        <h2 class="text-3xl font-semibold">Tasks List Application</h2>
      </RouterLink>
    </section>

    <section class="mt-6">
      <h3 class="font-medium text-sm uppercase">What is your task?</h3>

      <form @submit.prevent="addTask" class="w-full flex md:flex-row flex-col items-center gap-2 mt-3 bg-sky-900 md:rounded-2xl rounded-xl shadow-xl md:p-4 p-2">
        <input
          type="text"
          placeholder="e.g. have a stand up meeting"
          v-model="input_content"
          class="border border-slate-100 focus-within:outline-none bg-transparent flex flex-1 w-full md:rounded-2xl rounded-xl md:py-3 py-2 px-4 text-sm text-white"
        >

        <div class="flex md:w-auto w-full items-center gap-2">
          <input
            ref="dateInput"
            type="date"
            v-model="input_date"
            @focus="showDatePicker"
            :min="minDate"
            class="border border-slate-100 focus-within:outline-none bg-transparent flex w-full md:rounded-2xl rounded-xl md:py-3 py-2 px-4 text-sm text-white cursor-pointer"
          >
          <button type="submit" class="border border-slate-100 hover:bg-white/10 text-white rounded-full md:w-[48px] w-[38px] h-[38px] md:h-[48px] flex-shrink-0 font-bold text-xl">+</button>
        </div>
      </form>
    </section>

    <section class="mt-6 flex flex-col gap-2">
      <h3 class="font-medium text-sm uppercase">Tasks List</h3>

      <div v-if="paginatedTasks.length > 0" class="mt-1">
        <div class="flex flex-col gap-4">
          <TaskCard
            v-for="(task, index) in paginatedTasks"
            :key="`${task.title}_${index}`"
            :task="task"
            @remove="removeTask(task)"
          ></TaskCard>

        </div>

        <Pagination
          :currentPage="currentPage"
          :totalPages="totalPages"
          :changePage="changePage"
        ></Pagination>
      </div>

      <div v-else class="flex justify-center items-center md:p-10 p-3 md:py-10 py-4 text-center bg-sky-900 rounded-2xl mt-3 shadow-xl">
        <p class="opacity-60 md:text-base text-sm">You currently don't have any task on hand.<br>Create a new one to begin your productive day.</p>
      </div>
    </section>
  </main>
</template>