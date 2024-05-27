<template>
  <div>
    <h3>History</h3>
    <ul id="list" class="list">
      <li
        v-for="(transaction, index) in transactions"
        :key="index"
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
        @touchstart="startTouch($event, index)"
        @touchend="endTouch($event, index)"
      >
        {{ transaction.text }}
        <span>CHF {{ transaction.amount }}.-</span>
      </li>
    </ul>
  </div>
</template>


<script setup>
import { ref } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['delete-transaction']);

const touchStartX = ref(0);

const startTouch = (event, index) => {
  touchStartX.value = event.changedTouches[0].screenX;
};

const endTouch = (event, index) => {
  const touchEndX = event.changedTouches[0].screenX;
  if (touchEndX > touchStartX.value + 50) {
    emit('delete-transaction', props.transactions[index].id);
  }
};
</script>
