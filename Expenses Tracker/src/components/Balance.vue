<!-- Balance Component - Displays the current total balance -->
<template>
    <h4>Your Balance</h4>
    <h1 id="balance">${{ total }}</h1>
</template>

<script setup>
// Define props with validation
// total: The current balance to display, must be a number
 const props = defineProps({
   total:
   {
     type: Number,
     required: true
   }
 })
</script>
