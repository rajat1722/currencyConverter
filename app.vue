<template>
  <div class="">
    <div class="container1">
      <select class="border border-black" name="currency" id="currencyList" v-model="selectedCurrency1">
        
        <option v-for="name in computedCurrencyList1" :key="name" >{{ name }}</option>
      </select>

      <input class="block border-black" type="number" v-model="val1" placeholder="Enter Value" @input="changeVal2"> 
    </div>

    <div class="container2">
      <select class="border border-black" name="currency" id="currencyList" v-model="selectedCurrency2">
        
        <option v-for="name in computedCurrencyList2" :key="name" >{{ name }}</option>
      </select>
      <input class="block border-blue-50" type="number" v-model="val2" placeholder="Enter Value" @input="changeVal1">
       
    </div>
  
  </div>

</template>

<script setup lang="ts">
import type {currencies} from "./types/CurrencyListType"


// currencies and their value equivalent to 1 US Dollar
const currencyWithVal = {
  "Kuwaiti Dinar": 0.31,
  "Bahraini Dinar": 0.38,
  "Omani Rial": 0.39,
  "British Pound Sterling": 0.85,
  "European Euro": 0.98,
  "US Dollar": 1,
  "Brunei Dollar": 1.37,
  "New Zealand Dollar": 1.66,
  "Aruban Florin": 1.80,
  "Indian Rupee": 80.80
}

// arr of all currencies
const currencyNames = ref(["Kuwaiti Dinar", "Bahraini Dinar", "Omani Rial", "British Pound Sterling", "European Euro", "US Dollar", "Brunei Dollar", "New Zealand Dollar", "Aruban Florin", "Indian Rupee"])

// two selected currencies
let selectedCurrency1 = ref<currencies>("Kuwaiti Dinar")
let selectedCurrency2 = ref<currencies>("Indian Rupee")

// values of two selected currencies
let val1 = ref<number>()
let val2 = ref<number>()

// this removes selectedCurrency2 from computedCurrencyList1 
const computedCurrencyList1 = computed(() => {
  return currencyNames.value.filter((currency) => currency !== selectedCurrency2.value)
})

// this removes selectedCurrency1 from computedCurrencyList2
const computedCurrencyList2 = computed(() => {
  return currencyNames.value.filter((currency) => currency !== selectedCurrency1.value)
})
 

// this function calculates the value of val2 when val1 changes
function changeVal2(){
  val2.value = (val1.value! / currencyWithVal[selectedCurrency1.value]) * currencyWithVal[selectedCurrency2.value]
}

// this function calculates the value of val1 when val2 changes
function changeVal1(){
  val1.value = (val2.value! / currencyWithVal[selectedCurrency2.value]) * currencyWithVal[selectedCurrency1.value]
}
</script>

<style scoped>

</style>