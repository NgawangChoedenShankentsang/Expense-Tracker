<template>
    <h3>History</h3>
      <ul id="list" class="list">
        <li v-for="(transaction, index) in transactions" 
          :key="index" 
          :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
          {{transaction.text}}
            <span>CHF {{transaction.amount}}</span> 
            <button class="delete-btn" @click="deleteTransaction(transaction.id)">
              x
            </button>
        </li>

      </ul>
</template>

<script setup>
  import { defineProps } from 'vue'

  const props = defineProps({
    transactions: {
      type: Array,
      required: true,
    },
  });
  
  const emit = defineEmits(['delete-transaction']);

  const deleteTransaction = (id) => {
    emit('delete-transaction', id);
  };
</script>