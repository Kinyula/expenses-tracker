<script setup>
import { RouterLink, RouterView } from "vue-router";
import Header from "@/components/Header.vue";
import Balance from "@/components/Balance.vue";
import AddTransaction from "@/components/AddTransaction.vue";
import IncomeExpenses from "@/components/IncomeExpenses.vue";
import TransactionList from "@/components/TransactionList.vue";
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();

const transactions = ref([]);

onMounted(()=>{
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if(savedTransactions){
    transactions.value = savedTransactions;
  }
})

const total = computed(() => {
  return transactions.value.reduce((accumulator, transaction) => {
    return accumulator + transaction.amount;
  }, 0);
});

const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount < 0;
    })
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0)
    .toFixed(2);
});

const income = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount > 0;
    })
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0)
    .toFixed(2);
});
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  savedTransactionsToLocalStorage();
  toast.success("Transaction added...");
};

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => {
    return transaction.id !== id;
  });

  savedTransactionsToLocalStorage();
  toast.success("Transaction deleted...");
};

const savedTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
}
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :expenses="expenses" :income="income" />
    <TransactionList
      :transactions="transactions"
      @delete-transaction="handleTransactionDeleted" />
    <AddTransaction @transaction-submitted="handleTransactionSubmitted" />
  </div>
</template>

<style scoped></style>
