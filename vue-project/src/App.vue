<template>
  <div>
    <Header />
    <div class="container">
      <Balence :total="+total"/>
      <IncomeExpenses :income="+income" :expenses="+expenses"/>
      <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balence from './components/Balence.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import {ref, computed, onMounted} from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const transactions = ref([]);

onMounted(() =>{
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
})

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
});

const income = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount >= 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const expenses = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000)
}

const handleTransactionSubmitted = (transactionData) => {

  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  toast.success('transaction added')
}

const handleTransactionDeleted = (id) => {
  console.log(id)
  transactions.value = transactions.value.filter(transaction =>
    transaction.id !== id
  )

  toast.success('Transaction deleted')
}
</script>
