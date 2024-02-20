<template>
  <div>
    <Header />
    <div class="container">
      <Balence />
      <IncomeExpenses />
      <TransactionList :transactions="transactions"/>
      <AddTransaction />
    </div>
  </div>
</template>

<script setup>
 import Header from './components/Header.vue';
 import Balence from './components/Balence.vue';
 import IncomeExpenses from './components/IncomeExpenses.vue';
 import TransactionList from './components/TransactionList.vue';
 import AddTransaction from './components/AddTransaction.vue';

 import {ref} from 'vue';

 const transactions = ref([
      { id:1, text: 'Flower', amount: 20.00 },
      { id:2, text: 'Speaker', amount: -30.00 },
    ]);
</script>
