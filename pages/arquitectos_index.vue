<script>
  export default {
    async asyncData({ $content }) {
      const arquitectos = await $content('arquitectos').fetch()
      return {
        arquitectos
      }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <h3 style="margin-top: 15px">Información de Arquitectos</h3>
    <p>Esta sección presenta la información sobre los arquitectos</p>
   <ul>
     <li v-for="arquitecto in arquitectos" :key="arquitectos.slug">
       <NuxtLink :to="{ name: 'arquitectos-slug', params: { slug: arquitecto.slug } }">{{arquitecto.name}}</NuxtLink>
     </li>
   </ul>
   <FooterView />
 </div>
</template>