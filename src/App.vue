<template>
  <body>
    
    <HeaderComp 
      @startSearch = "startSearchApp"
    />

    <SliderComp 
      :posters = "trendigMovie"
    />
      
    <div class="container main-wrapper">


      <MainComp 
        v-if="movie.length > 0"
        titleCards = "FILM" :items="movie" :posters="movie"
      />

      <MainComp 
        v-if="tv.length > 0"
        titleCards = "SERIE TV" :items="tv" :posters="movie"
      />

    <h1 v-if="movie.length === 0 && tv.length === 0">Nessun risultato trovato</h1>
    </div>

  </body>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue'
import MainComp from './components/MainComp.vue'
import axios from 'axios'
import SliderComp from './components/SliderComp.vue'
// import { Carousel, CarouselItem } from 'vue-l-carousel'


export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp,
    SliderComp,
    // 'carousel': Carousel,
    // 'carouser-item': CarouselItem
  },

  data() {
    return {
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiParams: {
        api_key: '51a24be7274edb77373ac50e41995b10',
        language: 'it-IT',
        query: ''
      },
      movie: [],
      tv: [],
      trendigMovie: []
      
    }
  },

  methods: {
    getTrendingMovies(){
      axios.get( "https://api.themoviedb.org/3/trending/movie/week?api_key=" + this.apiParams.api_key)
      .then( res=> {
        console.log('TRENDING MOVIES:', res.data);
        this.trendigMovie = res.data.results;
        this.movie = res.data.results;
        console.log(this.trendigMovie);
      })
    },
    getTrendingSeries(){
      axios.get( "https://api.themoviedb.org/3/trending/tv/week?api_key=" + this.apiParams.api_key)
      .then( res=> {
        console.log('TRENDING SERIES:', res.data);
        this.tv = res.data.results;
      })
    },

    getApi(type){

      axios.get(this.apiUrl + type, {
          params: this.apiParams     
        }
      )

      .then(res => {
        //if(type === 'movie' || type !== 'all') this.tv = [];
        //else if( type === 'tv' || type !== 'all') this.movie = [];
        this[type] = res.data.results
      })

      .catch(err => {
        console.log(err);
      })
    },
    

    startSearchApp(titleToSearch, typeToSearch){
      this.movie = [];
      this.tv = [];
      this.apiParams.query = titleToSearch;
      if (titleToSearch.length > 0){
        if(typeToSearch === 'all'){
          this.getApi('movie');
          this.getApi('tv');
        }
        else {
          this.getApi(typeToSearch);
        }
      }
      else this.getTrendingMovies();
    }
    
  },

  mounted() {
    this.getTrendingMovies()
    this.getTrendingSeries()
  }

}
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap.scss';
  @import '~@fontsource/bebas-neue/index.css';
  @import '~@fortawesome/fontawesome-free/css/all.min.css';
  @import './assets/style/vars';


  body{
    font-family: "Bebas Neue", cursive;
    color: $font-color;
    background-color: $bg-color;
    .main-wrapper{
      padding-top: 90px;
    }
  }
</style>
