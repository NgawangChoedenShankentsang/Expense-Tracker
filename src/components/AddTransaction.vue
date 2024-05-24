<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Name</label>
      <input type="text" id="text" v-model="text" placeholder="Enter Name..." />
    </div>
    <div class="form-control">
      <label for="amount">Amount <br /></label>
      <input type="number" id="amount" v-model="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref, defineEmits } from 'vue';

const text = ref('');
const amount = ref('');

const toast = useToast();
const emit = defineEmits(['new-transaction']);
const onSubmit = async () => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled');
    return;
  }

  const newTransaction = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  try {
    const response = await fetch('https://json-server-job4.onrender.com/transactions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(newTransaction),
    });

    if (!response.ok) {
      throw new Error('Error adding transaction');
    }

    const addedTransaction = await response.json();
    emit('new-transaction', addedTransaction);

    text.value = '';
    amount.value = '';
    toast.success('Transaction added successfully');
  } catch (error) {
    toast.error(error.message);
    console.error(error);
  }
};
</script>
