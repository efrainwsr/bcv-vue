<script setup>
  import { ref, onMounted } from 'vue'
  import axios from 'axios'
  const url = 'https://bcv-api.vercel.app/bcv';
  const urlMenu = 'http://localhost:3000/menu';

  const bcvPrice = ref(0);
  const menu = ref(0);

   const obtenerBcv = onMounted( async ()=>{
   const { data } = await axios.get(url);
   console.log(data);
   bcvPrice.value = data.usd;
  })

   const getMenu = onMounted( async ()=>{
    const { data } = await axios.get(urlMenu);
    menu.value = data;
    console.log(data)

   })
</script>

<template>
  <div>
    <h1>Precio del BCV</h1>
    <p>{{ bcvPrice }}</p>
    <div v-for="item in menu">
      <p>{{item.nombre}} {{item.desc}} Precio: {{item.precio}}$</p>
    </div>
  </div>
</template>
  
