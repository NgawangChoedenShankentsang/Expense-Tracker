<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransaction from './components/AddTransaction.vue';

  import { ref, computed } from 'vue';

  const transactions = ref([
      { text: 'Flower', amount: -20 },
      { text: 'Salary', amount: 300 },
      { text: 'Book', amount: -10 },
      { text: 'Camera', amount: 150 },
  ]);

  
</script>