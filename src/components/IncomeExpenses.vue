<template>
  <div class="inc-exp-container">
    <div class="box income-box">
      <h4>Income</h4>
      <p id="money-plus" class="money plus">CHF {{ income }}.-</p>
    </div>
    <div class="box expense-box">
      <h4>Expense</h4>
      <p id="money-minus" class="money minus">CHF {{ expenses }}.-</p>
    </div>
  </div>
</template>

<script setup>
  import { defineProps } from 'vue'

  const props = defineProps({
    income: {
      type: Number,
      required: true,
    },
    expenses: {
      type: Number,
      required: true,
    }
  });
</script>