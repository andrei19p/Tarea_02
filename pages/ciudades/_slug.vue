<script>
export default {
  async asyncData({ $content, params }) {
    const ciudad = await $content('ciudades', params.slug).fetch();
    return { ciudad };
  },
  methods: {
    getSegmentsWithLinks(text) {
      const keywords = [
        { word: 'Burj Khalifa', url: '/edificios/edificio1' },
        { word: 'Merdeka 118', url: '/edificios/edificio2' },
        { word: 'Shanghai Tower', url: '/edificios/edificio3' },
        { word: 'Abraj Al Bait', url: '/edificios/edificio4' },
        { word: 'Ping An Finance Centre', url: '/edificios/edificio5' },
        { word: 'Lotte World Tower', url: '/edificios/edificio6' },
        { word: 'One World Trade Center', url: '/edificios/edificio7' },
        { word: 'Tianjin CTF Finance Centre', url: '/edificios/edificio8' },
        { word: 'Guangzhou CTF Finance Centre', url: '/edificios/edificio9' },
        { word: 'Central Park Tower', url: '/edificios/edificio10' },
        { word: 'Lakhta Center', url: '/edificios/edificio11' },
        { word: 'The Exchange 106', url: '/edificios/edificio12' }
      ];

      let result = [{ text: text, isLink: false }];

      keywords.forEach(keyword => {
        result = result.flatMap(segment => {
          if (segment.isLink) return [segment];
          const parts = segment.text.split(keyword.word);
          return parts.flatMap((part, index) => {
            return index < parts.length - 1
              ? [{ text: part, isLink: false }, { text: keyword.word, isLink: true, url: keyword.url }]
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
        <img class="u-max-full-width" :src="'/images/'+ciudad.image">
     </div>
     <div class="six columns">
       <h4>{{ciudad.name}}</h4>
       <b>Poblacion:</b> {{ciudad.poblacion}}</br>
       <b>Clima:</b> {{ciudad.clima}}</br>
       <b>Economia:</b> {{ciudad.economia}}</br>
       <b>Infraestructura:</b>
       <span>
        <span v-for="(segment, index) in getSegmentsWithLinks(ciudad.infraestructura)" :key="index">
            <template v-if="segment.isLink">
              <nuxt-link :to="segment.url">{{ segment.text }}</nuxt-link>
            </template>
            <template v-else>
              {{ segment.text }}
            </template>
          </span>
        </span>
	 </div>
	 <div class="two columns"></div>
   </div>
   <div id="comments"></div>
   <FooterView />
 </div>
</template>