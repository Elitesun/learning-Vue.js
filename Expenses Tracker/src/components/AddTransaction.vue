<!-- AddTransaction Component - Form for adding new transactions -->
<template>
  <h3>Add new transaction</h3>
   <!-- Instructions for users -->
   <h6>For income, enter a positive value (e.g., +100).<br />
    For expenses, enter a negative value (e.g., -50).</h6>
  <form id="form" @submit.prevent="onsubmit">
    <!-- Transaction description input -->
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text"  placeholder="Enter text..." v-model="text"/>
    </div> 
    <!-- Transaction amount input -->
    <div class="form-control">
      <label for="amount">
        Amount
      </label>
      <input type="number" id="amount"  placeholder="Enter amount..." v-model="amount"/>
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
// Import required Vue functionality and utilities
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

// Define emit event for new transaction submission
const emit = defineEmits(['TransactionSubmitted']);
const toast = useToast();

// Form input fields
const text = ref('');  // Description of the transaction
const amount = ref(''); // Amount of the transaction

/**
 * Handles the form submission for a new transaction
 * Validates input fields and emits the transaction data
 * Shows error toast if validation fails
 * Clears form after successful submission
 */
const onsubmit = () => {
    // Validate that both fields are filled
    if (!text.value || !amount.value) {
        toast.error('Both fields are required');
        return;
    }
    // Create transaction data object
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value),
    }
    // Emit event with transaction data
    emit('TransactionSubmitted', transactionData);
    // Clear form fields
    text.value = '';
    amount.value = '';
}
</script>
