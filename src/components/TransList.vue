<template>
  <h1 class="text-center font-bold text-xl">Transaction List</h1>
  <ul class="flex flex-col gap-2 items-center justify-center mt-2">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      class="flex items-center px-5 mx-2 py-1 rounded shadow w-2/3 bg-slate-200 border-l-4"
      :class="
        transaction.type === 'expense'
          ? 'border-l-red-500'
          : 'border-l-green-500'
      "
    >
      <h3 class="flex flex-col flex-1 items-start pl-2 font-medium">
        {{ transaction.title }}
        <span class="text-sm font-light">${{ transaction.amount }}</span>
      </h3>
      <i
        @click="onDeleteTransaction(transaction.id)"
        class="fa fa-trash text-red-600 hover:text-red-800 hover:cursor-pointer"
      ></i>
    </li>
  </ul>
</template>

<script setup lang="ts">
interface Transaction {
  id: number;
  type: string;
  title: string;
  amount: number;
}

const emits = defineEmits(["deleteTransaction"]);

defineProps({
  transactions: {
    type: Array as () => Transaction[],
    required: true,
  },
});

const onDeleteTransaction = (id) => {
  emits("deleteTransaction", id);
};
</script>

<style scoped></style>
