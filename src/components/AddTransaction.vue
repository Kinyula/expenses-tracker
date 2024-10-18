<script setup>
import { ref } from "vue"
import { useToast } from "vue-toastification";
const transactionText = ref("");
const transactionAmount = ref("");
const toast = useToast();
const emit = defineEmits(['transaction-submitted'])
const addTransaction = ()=> {
    if(!transactionText.value || !transactionAmount.value){
      
      toast.error("Please enter both transaction text and amount");
      return;
      
    }
    else{

      const transactionData = {
        text:transactionText.value,
        amount:parseFloat(transactionAmount.value)
      }

      emit('transaction-submitted', transactionData)
    }
}
</script>

<template>
  <div class="w-full max-w-lg bg-gray-50 shadow-lg rounded-lg p-8 mt-8">
      <h3 class="text-xl font-bold mb-4">Add New Transaction</h3>
      <form @submit.prevent="addTransaction">
        <div class="mb-4">
          <label for="text" class="block text-gray-700 font-medium mb-2">Transaction Text</label>
          <input 
            v-model="transactionText"
            type="text" 
            id="text"
            placeholder="Enter text..." 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
          />
        </div>
        <div class="mb-4">
          <label for="amount" class="block text-gray-700 font-medium mb-2">
            Amount <br />
            (negative - expense, positive - income)
          </label>
          <input 
            v-model="transactionAmount"
            type="text" 
            id="amount"
            placeholder="Enter amount..." 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
          />
        </div>
        <button
          type="submit"
          class="w-full bg-blue-500 text-white font-semibold py-2 rounded-md hover:bg-blue-600 transition duration-200"
        >
          Add Transaction
        </button>
      </form>
    </div>

</template>

<style scoped>

</style>