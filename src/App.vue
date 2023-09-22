<script setup>
  import { ref, onMounted,computed } from 'vue'
  import axios from 'axios'
  const url = 'https://bcv-apiv2.vercel.app/bcv';
  const urlMenu = 'https://bcv-apiv2.vercel.app/menu';

  const bcvPrice = ref(0);
  const menu = ref(0);
  const precioBS = ref(0);

   const obtenerBcv = onMounted( async ()=>{
   const { data } = await axios.get(url);
   console.log(data);
   bcvPrice.value = data.usd;
  })

   const getMenu = onMounted( async ()=>{
    const { data } = await axios.get(urlMenu);
    menu.value = data;
    console.log(data)

  /*  menu.value.forEach((item) => {
      let aux = bcvPrice.value(item.precio);
      item.bs = aux.toFixed(2)
    });*/

   })


      

</script>

<template>
  <!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carta de Restaurante</title>
    <link rel="stylesheet" href="estilos.css">
</head>

<body>
    <section id="menu">
        <h2>Menú</h2>
<table>
<tr>
   <th>Producto</th>
   <th>Precio $</th>
   <th>Precio Bs.</th>
</tr>
  <tr v-for="item in menu">
    <td>{{item.nombre}} {{item.desc}}</td>
    <td>{{item.precio}}</td>
    <td>{{(item.precio * bcvPrice).toFixed(2)}}</td>
  </tr>
</table>
    </section>
<h2>{{bcvPrice}}</h2>
</body>
</html>



  <!--
  <div>
    <h1>Tasa BCV {{bcvPrice}}</h1>
    <div v-for="item in menu">
      <p>{{item.nombre}} {{item.desc}} Precio: {{item.precio}}$</p>
    </div>
  </div>-->
</template>


<style scoped>
  /* Estilos generales */
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

.bcvPrice {
  margin-top: 15px ;
}

header {
    background-color: #333;
    color: #fff;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

nav ul {
    list-style: none;
    display: flex;
}

nav ul li {
    margin-right: 20px;
}



nav ul li a {
    color: #fff;
    text-decoration: none;
}

/* Estilos para las secciones */
/* Estilos para las secciones */
section {
    padding: 40px;
}

#menu .plato {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
}

.plato-info h3,
.plato-info p {
    margin: 0;
    margin-right: 20px;
}

.precio span {
    font-weight: bold;
    color: #ff6600;
}


/* Estilos para dispositivos móviles */
@media (max-width: 768px) {
    header {
        flex-direction: column;
        align-items: center;
    }

    nav ul {
        margin-top: 20px;
    }

    nav ul li {
        margin: 0;
    }

    section {
        padding: 20px;
    }
}

</style>
  
