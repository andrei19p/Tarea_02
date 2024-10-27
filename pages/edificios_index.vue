<script>
  export default {
    async asyncData({ $content }) {
      const edificios = await $content('edificios').fetch()
      return {
        edificios
      }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <h3 style="margin-top: 15px">Información de Edificios</h3>
   <p>Esta sección presenta la información sobre los edificios</p>
   <ul>
     <li v-for="edificio in edificios" :key="edificios.slug">
       <NuxtLink :to="{ name: 'edificios-slug', params: { slug: edificio.slug } }">{{edificio.name}}</NuxtLink>
     </li>
   </ul>
   <FooterView />
 </div>
</template>