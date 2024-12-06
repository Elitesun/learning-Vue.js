<!-- TransactionList Component - Displays the history of all transactions -->
<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <!-- Loop through transactions and display each one -->
    <li v-for="transaction in transactions" 
     :key="transaction.id"
     :class="transaction.amount > 0 ? 'plus' : 'minus' ">
      {{transaction.text}} 
      <span>
        {{transaction.amount > 0 ? '+' : ''}}{{transaction.amount}}$
      </span> 
      <!-- Delete button for each transaction -->
      <button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
    </li>
  </ul>
</template>

<script setup>
  // Define emit event for transaction deletion
  const emit = defineEmits(['TransactionDeleted']);

  // Define props with validation
  // transactions: Array of transaction objects to display
  const props = defineProps({
    transactions:
    {
      type: Array,
      required: true,
    },
  });

  /**
   * Emits an event to delete a transaction
   * @param {number} id The unique identifier of the transaction to delete
   */
  const deleteTransaction = (id) => {
    emit('TransactionDeleted', id);
  }
</script>
