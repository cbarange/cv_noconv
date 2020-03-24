<template>
  <div>
  <md-progress-bar v-if="pause" class="md-accent" md-mode="query"></md-progress-bar>
  <md-progress-bar v-else md-mode="determinate"></md-progress-bar>

    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  
  <md-card>
      <md-card-media>
        <img :src="items[currentIndex].img" alt="Image loading failed ... 😰">
      </md-card-media>

      <md-card-header>
        <div class="md-title">{{items[currentIndex].title}}</div>
        <div class="md-subhead">{{items[currentIndex].subtitle}}</div>
      </md-card-header>

      <md-card-expand>
        <md-card-actions md-alignment="space-between">
          <div>
            <md-button style="visibility: hidden">Action</md-button>
            <md-button style="visibility: hidden">Action</md-button>
          </div>

          <md-card-expand-trigger>
            <md-button class="md-icon-button">
              <md-icon>keyboard_arrow_down</md-icon>
            </md-button>
          </md-card-expand-trigger>
        </md-card-actions>

        <md-card-expand-content>
          <md-card-content>            
            {{items[currentIndex].text}}
          </md-card-content>
        </md-card-expand-content>
      </md-card-expand>
    </md-card>


  <div>
      <md-button v-if="currentIndex >0" @click="currentIndex >0 ? currentIndex -= 1 : null" class="md-fab md-primary">
        <md-icon>keyboard_arrow_left</md-icon>
      </md-button>
      <md-button v-else @click="currentIndex=items.length-1" class="md-fab md-primary">
        
        <md-icon>last_page</md-icon>
        
        
        
      </md-button>
      <md-button @click="pause=!pause" class="md-fab md-primary">
        <md-icon v-if="pause">pause</md-icon>
        <md-icon v-else>play_arrow</md-icon>
      </md-button>
      <md-button v-if="currentIndex < (items.length -1)" @click="currentIndex < (items.length -1)? currentIndex += 1 : null" class="md-fab md-primary">
        <md-icon>keyboard_arrow_right</md-icon>
      </md-button>
      <md-button v-else @click="currentIndex=0" class="md-fab md-primary">
        
        
        <md-icon>first_page</md-icon>
        
      </md-button>
      
    </div>
      <md-progress-bar v-if="pause" class="md-accent" md-mode="query"></md-progress-bar>
      <md-progress-bar v-else class="md-accent" md-mode="buffer"></md-progress-bar>

  </div>
</template>

<script>
import Vue from 'vue'
import VueMaterial from 'vue-material'

import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'
Vue.use(VueMaterial)
export default {
  name: 'HelloWorld',
  data () {
    return {
      pause:true,
      items:[
      {text:"Diplomé de l'IUT informatique de La Rochelle. Récemment accepté à l'école informatique de l'EPSI Nantes, en apprentissage chez Dassault Systemes ",
      title:'CV',
      subtitle:'Présentation',
      img:'https://www.guillenphoto.com/data/blog/2017/010-chronique-photo-minimaliste-8-techniques-I/images/photographie-minimaliste-d-un-mouflon-du-canada-dans-la-neige-yellowstone-wyoming-hiver.jpg'},

      {text:'https://www.linkedin.com/in/cl%C3%A9ment-baranger/',
      title:'Présentation',
      subtitle:'Linked-in',
      img:'https://salon-ctco.com/wp-content/uploads/2018/09/Logo-LinkedIn.png'},

      {text:'https://github.com/cbarange',
      title:'Présentation',
      subtitle:'GitHub',
      img:'https://upload.wikimedia.org/wikipedia/commons/thumb/9/91/Octicons-mark-github.svg/1200px-Octicons-mark-github.svg.png'},

      {text:'06 95 36 09 70 \n clementbaranger.pro@gmail.com',
      title:'Présentation',
      subtitle:'Contact',
      img:'https://www.espace-travertin.fr/wp-content/uploads/2017/01/contact-logo-download.png'},

      {text:'Java, SQL, JavaScript, HTML/CSS, C++, C, PHP, Python, SWIFT',
      title:'Compétences / Connaissances',
      subtitle:'Langages',
      img:'https://img2.freepng.fr/20180525/wvw/kisspng-web-development-logo-computer-programming-5b07d5d4af2bb4.0642809515272401487175.jpg'},

      {text:'Git, GNU/Linux, Windows, MySQL, Oracle DB, Docker, XML, UML, Qlik Sense, Trello, Développement agile (Scrum), Design pattern',
      title:'Compétences / Connaissances',
      subtitle:'Outils',
      img:'https://media.istockphoto.com/vectors/gear-and-repair-tool-logo-designs-inspiration-isolated-on-white-vector-id1054837900?k=6&m=1054837900&s=170667a&w=0&h=BKJ0aCdh2mnmwmHZbEzkubr0RLW0JZ6Ewrq2yWkL9mk='},
            
      {text:'JavaFX, JDBC, JUnit 4, Qt, SAX, DOM, Bootstrap, VueJs ,Contiki',
      title:'Compétences / Connaissances',
      subtitle:'API / Framework',
      img:'https://www.ixon.cloud/media/ciqpa3f3/api-2x.png'},

      {text:'Eclipse, Intellij, NetBeans, QtCreator, Keil uVision, PhpStorm, Octave',
      title:'Compétences / Connaissances',
      subtitle:'IDE',
      img:'https://media.istockphoto.com/vectors/gear-and-repair-tool-logo-designs-inspiration-isolated-on-white-vector-id1054837900?k=6&m=1054837900&s=170667a&w=0&h=BKJ0aCdh2mnmwmHZbEzkubr0RLW0JZ6Ewrq2yWkL9mk='},

       {text:'Développement d’une application Web de géo-visualisation - DUT CNRS de La Rochelle',
      title:'Expériences',
      subtitle:'Stage, 15 avril au 28 juin 2019',
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Développement d’une application sous Windows pour le département TC de l’IUT de La Rochelle',
      title:'Expériences',
      subtitle:'Projet de développement d’une éphéméride - DUT',
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Livraison de repas à domicile, Tours 37000 Société Deliveroo, en tant qu’auto-entrepreneur',
      title:'Expériences',
      subtitle:'Coursier à Vélo, été 2018',
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Castration de maïs, Angers 49000 Entreprise SCEA LE GILARD',
      title:'Expériences',
      subtitle:'Ouvrier Agricole, été 2016 et 2017',
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Ecole d’ingénierie informatique, Parcours DEVOPS, EPSI Nantes',
      title:' Formations / Diplômes',
      subtitle:'2019-2022',
      img:'https://lh3.googleusercontent.com/proxy/SXMz0wEhe7FE0DuMdBZuKxTQAr3I_rusXhj8jkAG7UMFSpkT-wnO7ZwzAsLg9fXJYb6qm3gMCY5IA_038sBrrxJR9PkOyXafqLh4bfa95Jyx6J9eWO5g5qYLyRuo-NX82rDoNC7x0qmx2EScWVWpX5iveT9p9gLafQk5LFfQAl8'},

      {text:'DUT Informatique, Parcours Environnement Connectés Intelligents Institut universitaire et technologique de La Rochelle',
      title:'Formations / Diplômes',
      subtitle:'2017-2019',
      img:'https://lh3.googleusercontent.com/proxy/SXMz0wEhe7FE0DuMdBZuKxTQAr3I_rusXhj8jkAG7UMFSpkT-wnO7ZwzAsLg9fXJYb6qm3gMCY5IA_038sBrrxJR9PkOyXafqLh4bfa95Jyx6J9eWO5g5qYLyRuo-NX82rDoNC7x0qmx2EScWVWpX5iveT9p9gLafQk5LFfQAl8'},

      {text:'Bac S option Sciences de l’Ingénieur spécialisation Informatique et sciences du numérique, mention bien , Lycée Grandmont Tours',
      title:'Formations / Diplômes',
      subtitle:'2016-2017 ',
      img:'https://lh3.googleusercontent.com/proxy/SXMz0wEhe7FE0DuMdBZuKxTQAr3I_rusXhj8jkAG7UMFSpkT-wnO7ZwzAsLg9fXJYb6qm3gMCY5IA_038sBrrxJR9PkOyXafqLh4bfa95Jyx6J9eWO5g5qYLyRuo-NX82rDoNC7x0qmx2EScWVWpX5iveT9p9gLafQk5LFfQAl8'},

      ],
      currentIndex:0
    }
  },
  methods: {},
  created: function () {},
  mounted: function () {},
  computed: {},
  watch: {}
}
</script>

<style scoped>
  .card-expansion {
    height: 480px;
  }
   .md-progress-bar {
    margin: 24px;
  }
  .md-card {
    width: 320px;
    margin: 4px;
    display: inline-block;
    vertical-align: top;
  }
</style>