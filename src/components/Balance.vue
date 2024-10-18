<script setup>
import {defineProps} from "vue"

const props = defineProps({
    total:{
        type:Number,
        required:true
    }
})
</script>

<template>
    <div class="w-full max-w-lg bg-gray-50 shadow-lg rounded-lg p-8 text-center">
      <h4 class="text-lg font-medium text-gray-700 mb-2">Your Balance</h4>
      <h1 class="text-4xl font-extrabold text-green-500">${{ total }}</h1>
    </div>
  </template>
  

<style scoped>

</style>