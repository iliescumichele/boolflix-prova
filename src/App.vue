<template>
  <div id="app">
    
    <headerComponent 
      @searchMovie="searchMovie" 
    />

    <mainComponent 
      :movie="filteredMovies"
    />
    
  </div>
</template>

<script>
import axios from 'axios'
import headerComponent from './components/headerComponent.vue'
import mainComponent from './components/mainComponent.vue'

export default {
  name: 'App',
  components: {
    headerComponent,
    mainComponent  
  },

  data(){
    
    return{
      trendingMoviesURL: 'https://api.themoviedb.org/3/trending/all/day?api_key=7c7fba51d38f79e494fc734298af352a',
      baseURL: 'https://api.themoviedb.org/3/search/movie/',
      apiParams:{
        api_key: '7c7fba51d38f79e494fc734298af352a',
        language: 'it-IT',
        query: ''
      },

      arrayTrendigMovies: [],
      filteredMovies: [],
    }
  },

  /////////////////////////////////////////////////////////////////

  methods:{
    printTrendingMovies(){
      axios.get(this.trendingMoviesURL
      )
      .then(response => {
        console.log('risposta dall \'API', response.data.results);
        this.filteredMovies = response.data.results;
        console.log('trending movies: ', this.arrayTrendigMovies)
      })
      .catch(error =>{
        console.log('errore nella richiesta api: ', error)
      })
    },

    sendApiRequest(){
      axios.get(this.baseURL,{
        params: this.apiParams
      })
      .then(response => {
        console.log('risposta dall \'API', response.data.results);
        this.filteredMovies = response.data.results;
      })
      .catch(error =>{
        console.log('errore nella richiesta api: ', error)
      })
    },

    searchMovie(textToSearch){
      this.apiParams.query = textToSearch;
      console.log(textToSearch);
      this.sendApiRequest(); 
    }
  },

  /////////////////////////////////////////////////////////////////

  computed:{
    searchedMovie(){
      let movieSearched = this.response.data.results;
      console.log('i film che sono stati cercati: ', movieSearched);
      return movieSearched
    }
  },
  
  /////////////////////////////////////////////////////////////////

  mounted(){
    this.printTrendingMovies();
  }
}
</script>

<style lang="scss">

  @import './assets/style/general.scss'

</style>
