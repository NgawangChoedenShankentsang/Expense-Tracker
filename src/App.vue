<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList :transactions="transactions" @delete-transaction="deleteTransaction" />
    <AddTransaction @new-transaction="addTransaction" />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed, onMounted } from 'vue';

const transactions = ref([]);

const fetchTransactions = async () => {
  try {
    const response = await fetch('http://localhost:5000/transactions');
    if (!response.ok) {
      throw new Error('Error fetching transactions');
    }
    const data = await response.json();
    transactions.value = data;
  } catch (error) {
    console.error('Error fetching transactions:', error);
  }
};

onMounted(fetchTransactions);

const addTransaction = (transaction) => {
  transactions.value.push(transaction);
};

const deleteTransaction = async (id) => {
  try {
    const response = await fetch(`http://localhost:5000/transactions/${id}`, {
      method: 'DELETE',
    });

    if (!response.ok) {
      throw new Error('Error deleting transaction');
    }

    transactions.value = transactions.value.filter(transaction => transaction.id !== id);
  } catch (error) {
    console.error('Error deleting transaction:', error);
  }
};

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
</script>
