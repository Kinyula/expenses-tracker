<script setup>
import {defineProps} from "vue"

const props = defineProps({
    transactions:{
        type:Array,
        required:true
    }
})

const emit = defineEmits(['delete-transaction']);

const deleteTransaction = (id) => {
    emit('delete-transaction', id);
}
</script>

<template>
   <div class="w-full max-w-lg">
      <h3 class="text-xl font-bold mb-4 border-b-2 border-gray-300 pb-2">History</h3>
      <ul>
        <li class="flex justify-between bg-white shadow-md p-4 rounded-lg mb-4 border-r-4" v-for="transaction in transactions" :key="transaction.id">
            {{ transaction.text }} <span>${{ transaction.amount }}</span><button @click="deleteTransaction(transaction.id)" class="bg-red-500 p-2 rounded-lg text-white">Delete</button>
        </li>
        <!-- <li class="flex justify-between bg-white shadow-md p-4 rounded-lg mb-4 border-r-4">
            Cash <span>$400</span><button class="bg-red-500 p-2 rounded-lg text-white">Delete</button>
        </li>

        <li class="flex justify-between bg-white shadow-md p-4 rounded-lg mb-4 border-r-4">
            Paycheck <span>$800</span><button class="bg-red-500 p-2 rounded-lg text-white">Delete</button>
        </li> -->

      </ul>
    </div>

</template>

<style scoped>

</style>