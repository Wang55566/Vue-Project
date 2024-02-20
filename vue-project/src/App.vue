<template>
  <Header />
  <div class="container">
    <Balence />
    <IncomeExpenses />
    <TransactionList />
    <AddTransaction />
  </div>
</template>

<script>
 import Header from './components/Header.vue';
 import Balence from './components/Balence.vue';
 import IncomeExpenses from './components/IncomeExpenses.vue';
 import TransactionList from './components/TransactionList.vue';
 import AddTransaction from './components/AddTransaction.vue';

 export default {
  components: {
    Header,
    Balence,
    IncomeExpenses,
    TransactionList,
    AddTransaction
  }
 }
</script>
