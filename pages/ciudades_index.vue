<script>
  export default {
    async asyncData({ $content }) {
      const ciudades = await $content('ciudades').fetch()
      return {
        ciudades
      }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <h3 style="margin-top: 15px">Información de Ciudades</h3>
   <p>Esta sección presenta la información sobre las ciudades</p>
   <ul>
     <li v-for="ciudad in ciudades" :key="ciudades.slug">
       <NuxtLink :to="{ name: 'ciudades-slug', params: { slug: ciudad.slug } }">{{ciudad.name}}</NuxtLink>
     </li>
   </ul>
   <FooterView />
 </div>
</template>