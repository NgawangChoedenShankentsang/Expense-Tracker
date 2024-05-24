<template>
  <div class="balance-container">
    <h4 class="balance-label">
        Your Balance
    </h4>
    <h1 id="balance">
        CHF {{ total }}.-
    </h1>
  </div>
</template>

<script setup>
  import { defineProps } from 'vue'

  const props = defineProps({
    total: {
      type: Number,
      required: true,
    },
  });
</script>