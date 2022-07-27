<template>
  
    <HeaderComp 
      @startSearch = "startSearchApp"
    />
    <MainComp 
      titleCards = "FILM" :items="movie"
    />

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
      apiUrl: 'https://api.themoviedb.org/3/search/movie',
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
      axios.get( "https://api.themoviedb.org/3/trending/all/week?api_key=" + this.apiParams.api_key)
      .then( res=> {
        console.log('TRENDING MOVIES:', res.data);
        this.movie = res.data.results;
      })
    },

    getApi(){
      axios.get(this.apiUrl, {
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

    startSearchApp(titleToSearch){
      this.apiParams.query = titleToSearch;
      this.getApi();
    }
    
  },

  mounted() {
    this.getTrendingMovies()
  }

}
</script>

<style lang="scss" scoped>

</style>
