<template>
  
    <HeaderComp />
    <MainComp />

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
      api_key: '51a24be7274edb77373ac50e41995b10',
      language: 'it-IT',
      query: 'harry potter'
      
    }
  },

  mounted() {
    this.getApi()
  },

  methods: {
    getApi(){
      axios.get(this.apiUrl, {
        params: {
          api_key: this.api_key,
          language: this.language,
          query: this.query
        }
      })
      
      .then(res => {
        console.log(res.data);
      })

      .catch(err => {
        console.log(err);
      })
    }
    
  }

}
</script>

<style>

</style>
