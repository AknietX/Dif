<script setup>
import axios from 'axios';
import { ref, inject } from 'vue';

const imageUrl1 = ref(null);
const imageUrl2 = ref(null);
const fileInput1 = ref(null);
const fileInput2 = ref(null);
const selectedFile1 = ref(null);
const selectedFile2 = ref(null);
const name = ref();
const { today, isCard } = inject('cart');

const handleFileChange1 = (event) => {
  const file = event.target.files[0];
  if (file) {
    selectedFile1.value = file;
    imageUrl1.value = URL.createObjectURL(file); // Превью первого фото
  }
};

const handleFileChange2 = (event) => {
  const file = event.target.files[0];
  if (file) {
    selectedFile2.value = file;
    imageUrl2.value = URL.createObjectURL(file); // Превью второго фото
  }
};

const openFilePicker1 = () => {
  fileInput1.value.click();
};

const openFilePicker2 = () => {
  fileInput2.value.click();
};

const provereno = ref();
const Proverka = (event) => {
  provereno.value = event.target.value;
};

const uploadPhoto = async () => {
  try {
    const response = await axios.post(`https://9e40d05721309bab.mokky.dev/${provereno.value}`, {
      imgScreen1: imageUrl1.value,
      imgScreen2: imageUrl2.value,
      Title: name.value,
      time: today.value,
    });

    console.log('Фото загружено:', response.data);

  } catch (error) {
    console.error('Ошибка загрузки:', error);
  }
};
const sure = ()=>{
  isCard.value = false
  uploadPhoto()
}
</script>

<template>
  <div class="absolute mt-0 ml-0 z-10 w-screen h-full bg-white flex items-center justify-center">
    <div>
      <div class="flex-col mb-4">
        <label for="name" class="block mb-1">Введите имя:</label>
        <input v-model="name" id="name" class="block border w-40 px-1 py-1" type="text" placeholder="текст...">

        <label for="city block">Выберите дело</label>
        <select v-on:change="Proverka" id="city" class="block border w-40 px-2 py-1">
          <option>Не выбрано</option>
          <option value="house">Весь дом</option>
          <option value="prih">Прихожка</option>
          <option value="posud">Посуда</option>
        </select>
      </div>

      <!-- Первое изображение -->
      <div class="mt-4 bg-black w-40 h-40">
        <img v-if="imageUrl1" :src="imageUrl1" alt="Превью 1" class="w-40 h-40 object-cover rounded shadow">
      </div>
      <input type="file" ref="fileInput1" @change="handleFileChange1" accept="image/*" class="hidden">
      <button @click="openFilePicker1" class="bg-blue-500 text-white px-4 py-2 rounded">Выбрать фото 1</button>

      <!-- Второе изображение -->
      <div class="mt-4 bg-black w-40 h-40">
        <img v-if="imageUrl2" :src="imageUrl2" alt="Превью 2" class="w-40 h-40 object-cover rounded shadow">
      </div>
      <input type="file" ref="fileInput2" @change="handleFileChange2" accept="image/*" class="hidden">
      <button @click="openFilePicker2" class="bg-blue-500 text-white px-4 py-2 rounded">Выбрать фото 2</button>

      <button @click="sure" class="mt-4 bg-green-500 text-white px-4 py-2 rounded">Готово</button>
    </div>
  </div>
</template>
