<script setup>
  import { ref, onMounted } from 'vue'
  import axios from 'axios'

  const bcvPrice = ref(0);

   const obtenerBcv = onMounted( async ()=>{
   const { data } = await axios.get('https://bcv-api.vercel.app/bcv');
   console.log(data);
   bcvPrice.value = data.usd;

  })

</script>
<template>
  <div>
    <h1>Precio del BCV</h1>
    <p>{{ bcvPrice }}</p>
  </div>
</template>
  
