<!-- pages/index.vue -->
<template>
  <div class="container">
    <HeaderView />
    <h2 style="margin-top: 15px">Catálogo de edificios más altos</h2>
     <p>Este website ofrece informacion sobre los edificios mas grandes de algunas ciudades y su arquitectos..</p>
     <ul>
       <li> <NuxtLink to="/edificios_index">Información de Edificos</NuxtLink></li>
       <li> <NuxtLink to="/ciudades_index">Información de Ciudades</NuxtLink></li>
       <li> <NuxtLink to="/arquitectos_index">Información de Arquitectos</NuxtLink></li>
     </ul>
    <FooterView />
  </div>
 </template>