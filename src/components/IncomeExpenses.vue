<script setup>
import {defineProps} from "vue"
const props = defineProps({
    expenses:{
        type:Number,
        required:true
    },
    income:{
        type:Number,
        required:true
    }
})
</script>

<template>
    <div class="w-full max-w-lg flex justify-between mt-8">
      <!-- Income Card -->
      <div class="w-1/2 bg-white shadow-md rounded-lg p-6 mr-2 text-center">
        <h3 class="text-lg font-semibold text-gray-600">Income</h3>
        <p class="text-2xl font-bold text-green-500">+${{ income }}</p>
      </div>

      <!-- Expense Card -->
      <div class="w-1/2 bg-white shadow-md rounded-lg p-6 ml-2 text-center">
        <h3 class="text-lg font-semibold text-gray-600">Expenses</h3>
        <p class="text-2xl font-bold text-red-500">-${{ expenses }}</p>
      </div>
    </div>

</template>

<style scoped>

</style>