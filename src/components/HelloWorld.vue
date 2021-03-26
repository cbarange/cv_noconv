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
      <md-card-content>            
        {{items[currentIndex].text}}
      </md-card-content>
  </md-card>

  <div>
      <md-button v-if="currentIndex >0" @click="previousCard()" class="md-fab md-primary">
        <md-icon>keyboard_arrow_left</md-icon>
      </md-button>
      <md-button v-else @click="lastCard()" class="md-fab md-primary">
        <md-icon>last_page</md-icon>
      </md-button>
      <md-button @click="pause=!pause" class="md-fab md-primary">
        <md-icon v-if="pause">pause</md-icon>
        <md-icon v-else>play_arrow</md-icon>
      </md-button>
      <md-button v-if="currentIndex < (items.length -1)" @click="nextCard()" class="md-fab md-primary">
        <md-icon>keyboard_arrow_right</md-icon>
      </md-button>
      <md-button v-else @click="firstCard()" class="md-fab md-primary">
        <md-icon>first_page</md-icon>
      </md-button>
    </div>
      <md-progress-bar v-if="pause" class="md-accent" md-mode="query"></md-progress-bar>
      <md-progress-bar v-else class="md-accent" md-mode="buffer"></md-progress-bar>

      <div>
        Ecouter dans un le même temps ma lettre de motivation ☺
      </div>
      <!--
      <button type="button" @click="audioPlay()" class="btn btn-default" ><i class="glyphicon glyphicon-play"></i> Play</button>
      <button type="button" @click="audioStop" class="btn btn-default"><i class="glyphicon glyphicon-stop"></i> Stop</button>
    -->
      <select v-model="voiceindex">
          <option v-for="voice in voiceselect" :value="voice.value">{{voice.text}}</option>
      </select>
  <div>

 <form>
    <table class="calc">
      <tbody>        
        <tr>
          <td>
            <textarea id="area" ref="area" :style="{fontSize: `${fontsize}px`}" rows="10" v-model="area" class="form-control">          
            </textarea>
          </td>
        </tr>
      </tbody>
    </table>
  </form>

</div>




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
    var s = { INIT:1, PLAY:2, PAUSED:3, END:4 }
    var vm = this
    return {
      pause:true,
      audioStatus:true,
      items:[
      {text:"Diplomé de l'IUT informatique de La Rochelle. Récemment accepté à l'école informatique de l'EPSI Nantes, en apprentissage chez Dassault Systemes ",
      title:'CV',
      subtitle:'Présentation',
      audio:'Candidature pour un poste de développeur Java junior, alternance informatique bachelor 3, EPSI.',
      audioTime:10000,
      img:'https://www.guillenphoto.com/data/blog/2017/010-chronique-photo-minimaliste-8-techniques-I/images/photographie-minimaliste-d-un-mouflon-du-canada-dans-la-neige-yellowstone-wyoming-hiver.jpg'},

      {text:'https://www.linkedin.com/in/cl%C3%A9ment-baranger/',
      title:'Présentation',
      subtitle:'Linked-in',
      audio:"Actuellement étudiant à l'IUT informatique de La Rochelle, j'ai la volonté de poursuivre mes études pour encore quelques années. Récemment accepté à l'école d’informatique, EPSI Nantes, je vais débuter une formation par alternance pour 3 années.",
      audioTime:20000,
      img:'https://salon-ctco.com/wp-content/uploads/2018/09/Logo-LinkedIn.png'
      },

      {text:'https://github.com/cbarange',
      title:'Présentation',
      subtitle:'GitHub',
      audio:"Je ne souhaite pas m'enfermer dans une technologie unique, mais bien appréhender un ensemble de compétences afin d'être le moins dépendant et le plus autonome possible.",
      audioTime:13000,
      img:'https://upload.wikimedia.org/wikipedia/commons/thumb/9/91/Octicons-mark-github.svg/1200px-Octicons-mark-github.svg.png'},

      {text:'06 95 36 09 70 \n clementbaranger.pro@gmail.com',
      title:'Présentation',
      subtitle:'Contact',
      audio:"Pour moi, l’alternance permet d’appliquer en milieu professionnel les connaissances acquises et d’obtenir un retour constructif. ",
      audioTime:10000,
      img:'https://www.espace-travertin.fr/wp-content/uploads/2017/01/contact-logo-download.png'},

      {text:'Java, SQL, JavaScript, HTML/CSS, C++, C, PHP, Python, SWIFT',
      title:'Compétences / Connaissances',
      subtitle:'Langages',
      audio:"Je cherche donc une entreprise prête à m’intégrer dans des projets concrets qui mettent en place ces connaissances.",
      audioTime:8000,
      img:'https://img2.freepng.fr/20180525/wvw/kisspng-web-development-logo-computer-programming-5b07d5d4af2bb4.0642809515272401487175.jpg'},

      {text:'Git, GNU/Linux, Windows, MySQL, Oracle DB, Docker, XML, UML, Qlik Sense, Trello, Développement agile (Scrum), Design pattern',
      title:'Compétences / Connaissances',
      subtitle:'Outils',
      audio:"J’ai une réelle volonté de continuer à accroître mon domaine de compétences ce qui m’amène à la recherche d’une entreprise pluridisciplinaire, qui n’hésite pas à adapter les technologies en fonction du besoin. ",
      audioTime:13000,
      img:'https://media.istockphoto.com/vectors/gear-and-repair-tool-logo-designs-inspiration-isolated-on-white-vector-id1054837900?k=6&m=1054837900&s=170667a&w=0&h=BKJ0aCdh2mnmwmHZbEzkubr0RLW0JZ6Ewrq2yWkL9mk='},
            
      {text:'JavaFX, JDBC, JUnit 4, Qt, SAX, DOM, Bootstrap, VueJs ,Contiki',
      title:'Compétences / Connaissances',
      subtitle:'API / Framework',
      audio:"Actuellement, mes compétences dominantes se retrouvent dans de la programmation Java, SQL avec des outils comme Git ou Docker et une ouverture sur le JavaScript.",
      audioTime:13000,
      img:'https://www.ixon.cloud/media/ciqpa3f3/api-2x.png'},

      {text:'Eclipse, Intellij, NetBeans, QtCreator, Keil uVision, PhpStorm, Octave',
      title:'Compétences / Connaissances',
      subtitle:'IDE',
      audio:"Je vous invite vraiment à vous rendre sur les liens que vous trouverez dans mon CV, vous y trouvez mes autres domaines et connaissances.",
      audioTime:11000,
      img:'https://media.istockphoto.com/vectors/gear-and-repair-tool-logo-designs-inspiration-isolated-on-white-vector-id1054837900?k=6&m=1054837900&s=170667a&w=0&h=BKJ0aCdh2mnmwmHZbEzkubr0RLW0JZ6Ewrq2yWkL9mk='},

       {text:'Développement d’une application Web de géo-visualisation - DUT CNRS de La Rochelle',
      title:'Expériences',
      subtitle:'Stage, 15 avril au 28 juin 2019',
      audio:"Durant les années à venir, je serais amené à choisir une coloration quant à la formation EPSI, mon choix se porte sur Le Big Data et la Sécurité Informatique. ",
      audioTime:13000,
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Développement d’une application sous Windows pour le département TC de l’IUT de La Rochelle',
      title:'Expériences',
      subtitle:'Projet de développement d’une éphéméride - DUT',
      audio:"Des compétences futures que je souhaite pouvoir mettre en œuvre durant l’alternance. ",
      audioTime:8000,
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Livraison de repas à domicile, Tours 37000 Société Deliveroo, en tant qu’auto-entrepreneur',
      title:'Expériences',
      subtitle:'Coursier à Vélo, été 2018',
      audio:'J’ai commencé au mois d’avril un stage de 11 semaines au CNRS de La Rochelle. Ce stage a pour objectif le développement d’une application web de visualisation de flux maritimes historiques.',
      audioTime:11000,
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Castration de maïs, Angers 49000 Entreprise SCEA LE GILARD',
      title:'Expériences',
      subtitle:'Ouvrier Agricole, été 2016 et 2017',
      audio:"Cela était ma première expérience professionnelle hors du cadre de l’IUT. Cette expérience m’apportera un premier retour sur la vie en entreprise. ",
      audioTime:11000,
      img:'https://img2.freepng.fr/20180407/zjw/kisspng-lumafox-creative-experience-national-waterways-mus-portfolio-5ac938d3a9ec98.289857851523136723696.jpg'},

      {text:'Ecole d’ingénierie informatique, Parcours DEVOPS, EPSI Nantes',
      title:' Formations / Diplômes',
      subtitle:'2019-2022',
      audio:"Ce stage a été pour moi l'occasion d'avancer dans ma formation professionnelle, de découvrir les contraintes et spécificités des projets de grandes tailles et de mieux appréhender la gestion de celui-ci.",
      audioTime:14000,
      img:'https://lh3.googleusercontent.com/proxy/SXMz0wEhe7FE0DuMdBZuKxTQAr3I_rusXhj8jkAG7UMFSpkT-wnO7ZwzAsLg9fXJYb6qm3gMCY5IA_038sBrrxJR9PkOyXafqLh4bfa95Jyx6J9eWO5g5qYLyRuo-NX82rDoNC7x0qmx2EScWVWpX5iveT9p9gLafQk5LFfQAl8'},

      {text:'DUT Informatique, Parcours Environnement Connectés Intelligents Institut universitaire et technologique de La Rochelle',
      title:'Formations / Diplômes',
      subtitle:'2017-2019',
      audio:"J’ai espoir que cette expérience puisse m’apporter un atout dans la recherche de l’alternance.",
      audioTime:9000,
      img:'https://lh3.googleusercontent.com/proxy/SXMz0wEhe7FE0DuMdBZuKxTQAr3I_rusXhj8jkAG7UMFSpkT-wnO7ZwzAsLg9fXJYb6qm3gMCY5IA_038sBrrxJR9PkOyXafqLh4bfa95Jyx6J9eWO5g5qYLyRuo-NX82rDoNC7x0qmx2EScWVWpX5iveT9p9gLafQk5LFfQAl8'},

      {text:'Bac S option Sciences de l’Ingénieur spécialisation Informatique et sciences du numérique, mention bien , Lycée Grandmont Tours',
      title:'Formations / Diplômes',
      subtitle:'2016-2017 ',
      audio:"En espérant avoir retenu votre attention. Je me tiens à votre disposition pour un rendez-vous ou appel téléphonique.",
      audioTime:10000,
      img:'https://lh3.googleusercontent.com/proxy/SXMz0wEhe7FE0DuMdBZuKxTQAr3I_rusXhj8jkAG7UMFSpkT-wnO7ZwzAsLg9fXJYb6qm3gMCY5IA_038sBrrxJR9PkOyXafqLh4bfa95Jyx6J9eWO5g5qYLyRuo-NX82rDoNC7x0qmx2EScWVWpX5iveT9p9gLafQk5LFfQAl8'},
      ],
      currentIndex:0,

      area:null,
      txt:'',
      fontsize:12,
      iplay: null, 
      previplay: null, 
      playstate:s.INIT,
      start: null,
      end: null,
      msg:null,
      imsg: null,
      voices:[],
      voiceindex:0,
      volume:null,
      back: false,
      play: false,
      
      forw: false,
      area: '',
      voiceselect: [],
      SpeechForm:{
        init(){
          vm.playstate = s.INIT;
          vm.back = false;
          vm.play = false;
          vm.forw = false;
          var area = vm.area
          vm.txt= area.replace(/\t/g,"");
          this.populateVoiceList();
        },
        populateVoiceList() {
          var voices = vm.SpeechSynth.getvoices();
          if( voices==null ) return;
          if( voices.length>21 ) voices.length=21;
          for(var i=0; i<voices.length; i++) {
            var textContent = voices[i].name + ' (' + voices[i].lang + ')';
            if( textContent.substring(0,6)=="Google" )
              textContent = textContent.substring(7,textContent.length);
            if( textContent.substring(0,9)=="Microsoft" )
              textContent = textContent.substring(10,textContent.length);
            vm.voiceselect.push({value: i, text: textContent});
          }
          i=1;
          if( voices.length>=4 ) i=4;
          //vm.SpeechSynth.setvoice(i-1);
        },
        copy()
        {
          vm.$refs.area.select();
          document.execCommand('copy');
        },
        zoomout()
        {
          vm.fontsize/=1.1;
        },
        zoomin()
        {
          vm.fontsize*=1.1;
        },
        resetform() {
          vm.SpeechSynth.stop();
          vm.area = ''
          vm.$refs.area.focus();
        },
        stopbtn() { 
        vm.SpeechSynth.stop();
        if( vm.playstate==s.INIT ) {
          vm.playstate=s.END;
          vm.SpeechForm.playmng();
        }
          else
            vm.playstate=s.END;
        },
        setselect() {
          if(vm.$refs.area){
            vm.$refs.area.selectionStart = vm.start;
            vm.$refs.area.selectionEnd = vm.end;
            vm.$refs.area.focus();
          }
          
        },
        playbtn() {
          if( vm.playstate==s.END ) vm.playstate = s.INIT;
          
          if( vm.playstate==s.INIT ) {
            vm.play = false
            vm.SpeechForm.playmng();
          }
          else if( vm.playstate==s.PLAY ) {
            vm.play = true
            vm.playstate=s.PAUSED;
            //SpeechSynth.pause();
            vm.SpeechSynth.stop();
            vm.SpeechForm.setselect();
          }
          else if( vm.playstate==s.PAUSED ) {
            vm.playstate = s.PLAY;
            vm.iplay--;
            vm.SpeechForm.playmng();
            vm.SpeechForm.setselect();
          }
        },
        pauseBtn(){
            vm.play = true
            vm.playstate=s.PAUSED;
            //SpeechSynth.pause();
            vm.SpeechSynth.stop();
            vm.SpeechForm.setselect();
          },
        playmng() {
          switch( vm.playstate ) {
            case s.INIT:
              vm.SpeechSynth.stop();
              if( vm.area=="" ) {
                vm.play = true
                return;
              }
              vm.txt=vm.area.replace(/([.?!:,\r\n])\s*/g, "$1|").split("|");
              if( vm.txt==null || vm.txt.length==0 ) {
                vm.play = true
                return;
              }
              vm.iplay = vm.start = vm.end = 0;
              vm.previplay = -1;
              vm.playstate = s.PLAY;
            case s.PLAY:
              var t=vm.txt[vm.iplay].replace(/[\"\'\’\‘]/gi, "");
              vm.SpeechSynth.play(t);
              if( vm.previplay != vm.iplay ) {
                vm.previplay = vm.iplay;
                vm.start = vm.area.indexOf(vm.txt[vm.iplay],vm.end);
                vm.end = vm.start+vm.txt[vm.iplay].length;
              }
              vm.SpeechForm.setselect();
              if( ++vm.iplay==vm.txt.length )
                vm.playstate = s.END;
              break;
            case s.PAUSED:
              break;
            case s.END:
              vm.play = false
              vm.$refs.area.blur();
              vm.playstate = s.INIT;
              break;
            default:
              console.log("Bad playstate!!!");
              
          }
        }
        
      },
      SpeechSynth:{
        init() {
          if( !('speechSynthesis' in window) ) {
            //alert("Speech synthesis is not supported in this browser!\nPlease use Chrome browser.");
            return;
          }
          vm.SpeechSynth.stop();
          vm.voices = window.speechSynthesis.getVoices();
          vm.volume=1.0;
          if (speechSynthesis.onvoiceschanged !== undefined) {
            speechSynthesis.onvoiceschanged = function() {
              console.log("onvoiceschanged()");
              if( vm.voices.length>0 ) return;
              vm.voices = window.speechSynthesis.getVoices()
              vm.SpeechForm.populateVoiceList();
            };
          }
        },
        getvoices() {
          return vm.voices;
        },
        setvolume(v) {
          vm.volume = v;
        },
        ispending() {
          return window.speechSynthesis.pending;
        },
        stop() {
          window.speechSynthesis.cancel();
        },
        pause() {
          //if( window.speechSynthesis.speaking )
          window.speechSynthesis.pause();
        },
        resume() {
          window.speechSynthesis.resume();
        },
        play(s) {
          //if( vm.voices.length==0 ) alert("No voices detected. Please restart the browser and try again.");
          vm.msg = new SpeechSynthesisUtterance();
          vm.msg.onend = function(e) {
            console.log('Finished in ' + e.elapsedTime + ' seconds.');
            vm.SpeechForm.playmng();
          };
          vm.msg.onerror = function(e) {
            console.log('Error in ' + e.elapsedTime + ' seconds.');
            vm.SpeechForm.playmng();
          };
          vm.msg.voice = vm.voices[vm.voiceindex];
          //msg.voiceURI = 'native';
          vm.msg.volume = vm.volume; // 0 to 1
          vm.msg.rate = 1.1; // 0.1 to 10
          vm.msg.pitch = 0; //0 to 2
          vm.msg.text = s;
          vm.msg.lang = vm.voices[vm.voiceindex].lang; //!!!
          //console.log(msg);
          window.speechSynthesis.speak(vm.msg);
          //setTimeout(function() { window.speechSynthesis.speak(msg); }, 0);
          if( ++vm.imsg==2 ) vm.imsg=0;
        }
      }
      
    }
    
  },
  methods: {
    doStuff:function() {
      if(this.pause && this.currentIndex<this.items.length-1 && this.iplay>=this.txt.length ){
        this.currentIndex+=1
        this.area=this.items[this.currentIndex].audio
        this.audioStatus?this.SpeechForm.playbtn():this.SpeechForm.pauseBtn()
      }
      setTimeout(this.doStuff, 1000);
    },
    audioPlay:function(){
      this.audioStatus=true
      this.SpeechForm.playbtn()
    },
    audioStop:function(){
      this.audioStatus=false
      this.SpeechForm.pauseBtn()
    },
    previousCard:function(){
      this.currentIndex > 0 ? this.currentIndex -= 1 : null
      this.area=this.items[this.currentIndex].audio
    },
    nextCard:function(){
      this.currentIndex < this.items.length-1 ? this.currentIndex += 1 : null
      this.area=this.items[this.currentIndex].audio
    },
    firstCard:function(){
      this.currentIndex = 0
      this.area=this.items[this.currentIndex].audio
    },
    lastCard:function(){
      this.currentIndex =this.items.length-1
      this.area=this.items[this.currentIndex].audio
    }
  },
  created: function () {},
  mounted: function () {
    setTimeout(this.doStuff, 10000)
    var vm = this
    vm.SpeechSynth.init()
    vm.SpeechForm.init()
    this.area=this.items[this.currentIndex].audio
    this.SpeechForm.playbtn()
  },
  computed: {},
  watch: {
    pause:function(){
      if(this.pause)
        this.audioPlay()
      else
        this.audioStop()

    }
  }
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
  form{
    width: 55%;
    margin-left:23%;
  }
  .calc{
    width:100%;
  }
  #area{
    resize: none;
    width: 100%;
  }
</style>