<template>
  
    <HeaderComp 
      @startSearch = "startSearchApp"
    />
    <MainComp 
      v-if="movie.length > 0"
      titleCards = "FILM" :items="movie"
    />
    <MainComp 
      v-if="serieTv.length > 0"
      titleCards = "SERIE TV" :items="serieTv"
    />

    <h1 v-if="movie.length === 0 && serieTv.length > 0">Nessun risultato</h1>

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
      apiUrlMovie: 'https://api.themoviedb.org/3/search/movie',
      apiUrlSeries: 'https://api.themoviedb.org/3/search/tv',
      apiParams: {
        api_key: '51a24be7274edb77373ac50e41995b10',
        language: 'it-IT',
        query: ''
      },
      movie: [],
      serieTv: [],
      
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
        this.serieTv = res.data.results;
      })
    },

    getApiMovie(){
      axios.get(this.apiUrlMovie, {
          params: this.apiParams     
        }
      )

      .then(res => {
        this.movie = res.data.results
      })

      .catch(err => {
        console.log(err);
      })
    },
    getApiSeries(){
      axios.get(this.apiUrlSeries, {
          params: this.apiParams     
        }
      )

      .then(res => {
        this.serieTv = res.data.results
      })

      .catch(err => {
        console.log(err);
      })
    },

    startSearchApp(titleToSearch){
      this.apiParams.query = titleToSearch;
      if (titleToSearch.length > 0){
        this.getApiMovie();
        this.getApiSeries();
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

<style lang="scss" scoped>

</style>
