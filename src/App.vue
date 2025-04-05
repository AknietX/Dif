<script setup>
import { computed, onMounted, provide } from 'vue';
import { ref } from 'vue';
import drawer from './components/drawer.vue'
import posud from './components/posud.vue';
import axios from 'axios';
import prih from './components/prih.vue';

import house from './components/house.vue';
const today = ref(computed(() => new Date().toLocaleDateString()))
const items = ref([])
const priha = ref([])
const house1 = ref([])
const isCard = ref(false)


provide('cart', {
  isCard,
  items,
  priha,
  today,
  house1

})



const fetchPrih = async()=>{
  try{
    const {data} = await axios.get('https://9e40d05721309bab.mokky.dev/prih')
    priha.value = data
  }catch(err){
    console.log(err)
  }
}
const fetchHouse = async()=>{
  try{
    const {data} = await axios.get('https://9e40d05721309bab.mokky.dev/house')
    house1.value = data

  }catch(err){
    console.log(err)
  }
}
onMounted(async ()=>{
  try{
    const {data} = await axios.get('https://9e40d05721309bab.mokky.dev/posud')
    items.value = data
    await fetchPrih()
    await fetchHouse()



  }
  catch(err){
    console.log(err)
  }
})
</script>

<template>
  <div class="w-full h-full bg-[#FFAD73] relative">
    <drawer v-if="isCard" />


    <div class="w-full flex justify-center  items-center border-b border-slate-300">
      <h1 class="text-[30px] text-[#b0eeff]">Число: {{ today }}</h1>
    </div>
    <main class="mt-10 z-10 pl-10 pr-10 grid grid-cols-2 gap-1 gap-y-7 items-center">

        <posud />

        <prih />
      <div class="px-4 h-120 text-[#b0eeff] border py-4 w-50">
        <span>
          не рабочий
        </span>
        <ul class="max-h-100 overflow-y-auto w-50">
          <li>2</li>
          <li>3</li>

        </ul>
        <button class="border rounded-[3px] px-10 py-2 bg-[#FF9640]">Добавить</button>
      </div>
      <house />

    </main>
  </div>
</template>

