<template>
  <body>
    
    <HeaderComp 
      @startSearch = "startSearchApp"
    />

    <div class="container main-wrapper">

      <MainComp 
        v-if="movie.length > 0"
        titleCards = "FILM" :items="movie"
      />

      <MainComp 
        v-if="tv.length > 0"
        titleCards = "SERIE TV" :items="tv"
      />

    </div>

    <h1 v-if="movie.length === 0 && tv.length === 0">Nessun risultato</h1>
  </body>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue'
import MainComp from './components/MainComp.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp,
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
      
    }
  },

  methods: {
    getTrendingMovies(){
      axios.get( "https://api.themoviedb.org/3/trending/movie/week?api_key=" + this.apiParams.api_key)
      .then( res=> {
        console.log('TRENDING MOVIES:', res.data);
        this.movie = res.data.results;
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
