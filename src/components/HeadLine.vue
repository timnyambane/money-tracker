<template>
  <div class="flex flex-col items-center">
    <h1 class="w-1/3 py-3 bg-slate-100 rounded-md text-center">
      Balance: <span class="font-bold">$ {{ total }}</span>
    </h1>

    <div class="flex justify-between m-2 w-1/2">
      <div class="flex flex-col items-center border-r-2 px-8 flex-1">
        Income: <span class="font-bold text-green-600">$ {{ income }}</span>
      </div>
      <div class="flex flex-col items-center px-8 flex-1">
        Expense: <span class="font-bold text-red-600">$ {{ expense }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({
  income: {
    type: Number,
    default: 0,
  },
  expense: {
    type: Number,
    default: 0,
  },
  total: {
    type: Number,
    default: 0,
  },
});
</script>

<style scoped></style>
