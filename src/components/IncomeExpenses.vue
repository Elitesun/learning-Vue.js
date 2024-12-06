<!-- IncomeExpenses Component - Displays the summary of income and expenses -->
<template>
  <div class="inc-exp-container">
    <div>
        <h4 id="income">Income</h4>
        <p id="money-plus" class="money plus">+ ${{ income }}</p>
    </div>
    <div>
        <h4 id="expense">Expenses</h4>
        <p id="money-minus" class="money minus"> $ -{{ expense }}</p>
    </div>
  </div>
</template>

<script setup>
// Define props with validation
// income: Total positive transactions (money received)
// expense: Total negative transactions (money spent)
const props = defineProps({
  income:
  {
    type: Number,
    required: true,
  },
  expense:
  {
    type: Number,
    required: true,
  },
});

</script>
