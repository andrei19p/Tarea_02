<script>
export default {
  async asyncData({ $content, params }) {
    const arquitecto = await $content('arquitectos', params.slug).fetch();
    return { arquitecto };
  },
  methods: {
    getObrasWithLinks(obras) {
      const notableWorks = [
      { name: 'Burj Khalifa', url: '/edificios/edificio1' },
      { name: 'Merdeka 118', url: '/edificios/edificio2' },
      { name: 'Shanghai Tower', url: '/edificios/edificio3' },
      { name: 'Abraj Al Bait', url: '/edificios/edificio4' },
      { name: 'Ping An Finance Centre', url: '/edificios/edificio5' },
      { name: 'Lotte World Tower', url: '/edificios/edificio6' },
      { name: 'One World Trade Center', url: '/edificios/edificio7' },
      { name: 'Tianjin CTF Finance Centre', url: '/edificios/edificio8' },
      { name: 'Guangzhou CTF Finance Centre', url: '/edificios/edificio9' },
      { name: 'Central Park Tower', url: '/edificios/edificio10' },
      { name: 'Lakhta Center', url: '/edificios/edificio11' },
      { name: 'The Exchange 106', url: '/edificios/edificio12' }
      ];

      let result = [{ text: obras, isLink: false }];

      notableWorks.forEach(work => {
        result = result.flatMap(segment => {
          if (segment.isLink) return [segment];
          const parts = segment.text.split(work.name);
          return parts.flatMap((part, index) => {
            return index < parts.length - 1
              ? [{ text: part, isLink: false }, { text: work.name, isLink: true, url: work.url }]
              : [{ text: part, isLink: false }];
          });
        });
      });

      return result;
    }
  },
  mounted() {
  setTimeout(() => {
    const script = document.createElement('script');
    script.src = "https://utteranc.es/client.js";
    script.setAttribute("repo", "andrei19p/Tarea_02");
    script.setAttribute("issue-term", "pathname");
    script.setAttribute("theme", "github-light");
    script.setAttribute("crossorigin", "anonymous");
    script.async = true;

    const commentsContainer = document.getElementById('comments');
    if (commentsContainer) {
      commentsContainer.appendChild(script);
    }
  });
}
}
</script>

<template>
  <div class="container">
   <HeaderView />
   <div class="row">
     <div class="three columns">
        <img class="u-max-full-width" :src="'/images/'+arquitecto.image">
     </div>
     <div class="six columns">
       <h4>{{arquitecto.name}}</h4>
      <b>Nacionalidad:</b> {{arquitecto.nacionalidad}}</br>
      <b>Estilo:</b> {{arquitecto.estilo}}</br>
      <b>Obras Notables:</b>
        <span>
          <span v-for="(segment, index) in getObrasWithLinks(arquitecto.obras_notables)" :key="index">
            <template v-if="segment.isLink">
              <!-- Si es un enlace, usamos nuxt-link -->
              <nuxt-link :to="segment.url">{{ segment.text }}</nuxt-link>
            </template>
            <template v-else>
              {{ segment.text }}
            </template>
          </span>
        </span>
        </br>
      <b>Distincion:</b> {{arquitecto.distincion}}
	 </div>
	 <div class="two columns"></div>
   </div>
   <div id="comments"></div>
   <FooterView />
 </div>
</template>