<template>
  <div class="container mx-auto py-2 my-2 border w-2/3">
    <h1 class="font-extrabold underline p-2 text-center text-4xl">
      Money Tracker
    </h1>
    <HeadLine :income="income" :expense="expense" :total="total" />
    <FormInputs @submit-transaction="handleSubmitTransaction" />
    <TransList
      :transactions="transactions"
      @delete-transaction="handleDeleteTransaction"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from "vue";

import FormInputs from "./components/FormInputs.vue";
import HeadLine from "./components/HeadLine.vue";
import TransList from "./components/TransList.vue";

interface Transaction {
  id: number;
  type: string;
  title: string;
  amount: number;
}
const transactions = ref<Array<Transaction>>([]);

onMounted(() => {
  const savedTransactions = JSON.parse(
    localStorage.getItem("transactions") || "null"
  );
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const total = computed(() => {
  const totalAssets = transactions.value
    .filter((transaction) => transaction.type === "income")
    .reduce((acc, transaction) => acc + transaction.amount, 0);

  const totalExpenses = transactions.value
    .filter((transaction) => transaction.type === "expense")
    .reduce((acc, transaction) => acc + transaction.amount, 0);

  return totalAssets - totalExpenses;
});

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.type === "income")
    .reduce((acc, transaction) => transaction.amount, 0);
});

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.type === "expense")
    .reduce((acc, transaction) => transaction.amount, 0);
});

const handleSubmitTransaction = (transactionData) => {
  transactions.value.push(transactionData);

  saveTransactionstoLS();
};

const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionstoLS();
};

const saveTransactionstoLS = () =>
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
</script>

<style scoped></style>
