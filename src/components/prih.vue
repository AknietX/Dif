<script setup>
import { inject, } from 'vue';

const { priha, isCard } = inject('cart')

const checkCard = ()=>{
    isCard.value = true
}
</script>

<template>


<div class="px-4 h-120 text-[#b0eeff] border py-4 w-50">
        <span>
          Прихожка:
        </span>
        <ul class="max-h-100 overflow-y-auto w-50">
          <li class="w-40 text-white mb-1" v-for="item in priha" :key="item.id" :class="item.imgScreen ? 'bg-[#7fe5ba]' : 'bg-[#ff6f69]'" >{{ item.Title }} {{ item.time }}</li>
        </ul>
        <button :disabled="false" @click="checkCard" class="cursor-pointer active:bg-black border rounded-[3px] px-10 disabled:bg-[#879eb0] active:bg-[#FF9640] py-2 bg-[#FF9640]">Добавить</button>

      </div>
</template>
