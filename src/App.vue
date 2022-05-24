<template>
  <div id="app">
    
    <headerComponent 
      @searchText="searchMovieSerie" 
      @selectMovieOrSerieTV='searchWithSelect'
    />

    <mainComponent 
      :movie="arrayMovies"
      :trends="arrayTrends"
      :tvSeries="arrayTvSeries"
      :txtFromSelect="textfromSelect"
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
      trendingAllURL: 'https://api.themoviedb.org/3/trending/all/day?api_key=7c7fba51d38f79e494fc734298af352a',
      trendingMoviesURL: 'https://api.themoviedb.org/3/trending/movie/day?api_key=7c7fba51d38f79e494fc734298af352a',
      trendingTvURL: 'https://api.themoviedb.org/3/trending/tv/day?api_key=7c7fba51d38f79e494fc734298af352a',

      baseUrlMovie: 'https://api.themoviedb.org/3/search/movie/',
      baseUrlTvSeries: 'https://api.themoviedb.org/3/search/tv',
      apiParams:{
        api_key: '7c7fba51d38f79e494fc734298af352a',
        language: 'it-IT',
        query: ''
      },

      arrayMovies: [],
      arrayTvSeries: [],
      arrayTrends: [],
      textFromSelect: ''
    }
  },

  /////////////////////////////////////////////////////////////////

  methods:{
    printTrending(){
      axios.get(this.trendingAllURL
      )
      .then(response => {
        console.log('risposta dall \'API', response.data.results);
        this.arrayTrends = response.data.results;
        console.log('trending movies: ', this.arrayTrends)
      })
      .catch(error =>{
        console.log('errore nella richiesta api: ', error)
      })
    },

    sendApiRequest(urlApi){
      axios.get(urlApi,{
        params: this.apiParams
      })
      .then(response => {
        console.log('risposta dall \'API', response.data.results);
        if(urlApi === this.baseUrlMovie) {
          this.arrayMovies = response.data.results;
        }
        else if (urlApi === this.baseUrlTvSeries) {
          this.arrayTvSeries = response.data.results;
        }
        else{
          this.arrayTrends = response.data.results;
        }
      })
      .catch(error =>{
        console.log('errore nella richiesta api: ', error)
      })
    },

    searchMovieSerie(textToSearch){
      this.apiParams.query = textToSearch;
      console.log('text to search>>> ', textToSearch);
      this.searchWithSelect(this.textFromSelect); 
    },


    searchWithSelect(dataFromSelectedComp){
      this.textFromSelect = dataFromSelectedComp;
      if(dataFromSelectedComp === 'Movie'){
        this.sendApiRequest(this.trendingMovieURL)
      }
      else if(dataFromSelectedComp === 'TV'){
        this.sendApiRequest(this.trendingTvURL)
      }
      else{
        this.sendApiRequest(this.trendingAllURL)
      }
    }
  },

  /////////////////////////////////////////////////////////////////

  computed:{
    searchedMovie(){
      let movieSearched = this.response.data.results;
      return movieSearched
    }  
  },
  
  /////////////////////////////////////////////////////////////////

  mounted(){
    this.searchWithSelect('');
  }
}
</script>

<style lang="scss">

  @import './assets/style/general.scss'

</style>
