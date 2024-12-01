<!-- Main App Component - Manages the overall expense tracking functionality -->
<template>
  <div class="container">
    <Header/>
    <!-- Display total balance -->
    <Balance :total="+total"/>
    <!-- Display income and expense summary -->
    <IncomeExpenses :income="+income" :expense="+expense"/>
    <!-- List of transactions with delete functionality -->
    <TransactionList :transactions="transactions" @TransactionDeleted="deleteTransaction"/>
    <!-- Form to add new transactions -->
    <AddTransaction @TransactionSubmitted="addTransaction"/>
  </div>
</template>

<script setup>
// Import required Vue functionality and components
import { ref, computed , onMounted} from 'vue'
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

// Import toast notification functionality
import { useToast } from 'vue-toastification';

const toast = useToast();

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const transactions = ref([]);

// calculating total balance
const total = computed(() => {
  return transactions.value
  .reduce((acc, transaction) => acc + transaction.amount, 0)
})

//  computing income
const income = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
})
// expenses
const expense = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => acc + Math.abs(transaction.amount), 0)
    .toFixed(2);
})

// Delete a transaction by its ID
const deleteTransaction = (id) => {
  transactions.value = transactions.value
  .filter(transaction => transaction.id !== id);

  saveTransactionsToLocalStorage();
  toast.success('Transaction deleted.');
}

// Add a new transaction to the list
const addTransaction = (transaction) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transaction.text,
    amount: transaction.amount
  });
  saveTransactionsToLocalStorage();
  toast.success('Transaction added.');
}

// Generate a random ID for new transactions
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Save transactions to localStorage for persistence
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};



</script>
