<template>
  <div id="app">

    <Header @sendSearch="startSearch" />

    <div class="container" v-if="movie.length === 0 && tv.length === 0">
      <h2>Nessun risultato trovato</h2>
    </div>
    <div v-else>
      <Main v-if="movie.length > 0" :listResult="movie" titleSection="Film"  />
      <Main v-if="tv.length > 0" :listResult="tv" titleSection="Serie TV"  />
    </div>
    

  </div>
</template>

<script>

import axios from 'axios'

import Header from './components/Header'
import Main from './components/Main'

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data(){
    return{
      movie:[],
      tv: [],
      type:'',
      apiUrl: 'https://api.themoviedb.org/3/search/',
      apiParams :{
        api_key: '1b3eb153fce73eb6b953f7d515b2dc1d',
        language: 'it-IT',
        query: ''
      }
    }

  },
  methods:{
    getApi(type, isPopular = false ){
      let apiUrlGeneratad = '';
      if(!isPopular) apiUrlGeneratad = this.apiUrl+type;
      else {
        apiUrlGeneratad = 'https://api.themoviedb.org/3/movie/popular';
      }
      axios.get(apiUrlGeneratad, {params: this.apiParams})
      .then(res => {
        this[type] = res.data.results;
      })
      .catch(err => {
        console.log(err);
      })
    },
    startSearch(text, type){
      this.movie = [];
      this.tv = [];
      this.apiParams.query = text;
      if(type === ''){
        this.getApi('movie');
        this.getApi('tv');
      }else{
        this.getApi(type);
      }
      
    }
  },
  mounted(){
    this.getApi('movie',true);
  }
}
</script>

<style lang="scss">

@import './assets/style/vars.scss';
@import './assets/style/general.scss';

</style>
