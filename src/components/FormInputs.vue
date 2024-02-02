<template>
  <form
    @submit.prevent="addTransaction"
    class="w-5/6 mx-auto border py-3 flex flex-col gap-1 items-center"
  >
    <div class="flex gap-1 justify-center">
      <select
        name=""
        id=""
        class="form-select py-2 rounded-md border"
        v-model="transType"
      >
        <option value="" disabled selected>Select option</option>
        <option value="expense">Expense</option>
        <option value="income">Income</option>
      </select>

      <input
        v-model="title"
        type="text"
        placeholder="Enter Title"
        class="form-input px-2 rounded-md border w-1/2"
      />

      <input
        v-model="amount"
        type="number"
        placeholder="Enter Amount"
        class="form-input px-2 rounded-md border w-1/4"
      />
    </div>
    <button
      type="submit"
      class="bg-blue-500 px-3 py-1 w-2/3 my-2 text-white rounded hover:bg-blue-600"
    >
      Add
    </button>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const transType = ref("");
const title = ref("");
const amount = ref("");

const emit = defineEmits(["submitTransaction"]);

const addTransaction = () => {
  if (!transType.value || !title.value || !amount.value) {
    alert("Please fill in all fields before adding a transaction.");
    return;
  }

  const newTransaction = {
    id: uuidv4(),
    type: transType.value,
    title: title.value,
    amount: amount.value,
  };
  emit("submitTransaction", newTransaction);

  transType.value = "";
  title.value = "";
  amount.value = "";
};
</script>

<style scoped></style>
