<script>
export default {
  props: {
    currentPage: Number,
    totalPages: Number,
    changePage: Function,
  },
};
</script>

<template>
  <div class="mt-4 flex justify-between items-center gap-2 md:text-base text-sm">
    <button
      :disabled="currentPage === 1"
      @click="changePage(currentPage - 1)"
      class="text-white opacity-70 cursor-pointer hover:opacity-50 disabled:opacity-30"
    >
      Prev
    </button>

    <div class="flex justify-center items-center">
      <button
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        @click="changePage(pageNumber)"
        :class="{ 'bg-sky-500 shadow-sky-600 text-white': currentPage === pageNumber, 'text-white bg-opacity-20 hover:bg-opacity-40 bg-white cursor-pointer': currentPage !== pageNumber }"
        class="md:h-10 md:w-10 h-8 w-8 rounded-full mx-1 shadow-md"
      >
        {{ pageNumber }}
      </button>
    </div>

    <button
      :disabled="currentPage >= totalPages"
      @click="changePage(currentPage + 1)"
      class="text-white opacity-70 cursor-pointer hover:opacity-50 disabled:opacity-30"
    >
      Next
    </button>
  </div>
</template>