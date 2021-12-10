<template>
  <FlipFlopCard 
    :width="300"
     class="sc-card">
     <template slot="front">
       <div class="inner">
         <img 
            class="cover"
            v-if="item.poster_path"
            :src="`https://image.tmdb.org/t/p/w342/${item.poster_path}`" 
            :alt="item.title || item.name">
          <div v-else>
            <h2>{{item.title || item.name}}</h2>
            <img class="cover" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png" alt="no image">
          </div>
       </div>
     </template>

     <template slot="back">
       <div class="inner">
         <div class="inner-back">
          <h2>{{item.title || item.name}}</h2>
          
          <h5>{{item.original_title || item.original_name}}</h5>
          <div>
            <img 
            class="flag"
              v-if="flags.includes(item.original_language)"
              :src="require(`../assets/img/${item.original_language}.png`)" 
              :alt="item.title">
            <p v-else>Lingua: {{item.original_language}}</p>
          </div>
          <div>
            <i 
            v-for="(intem, index) in 5"
            :key="index"
            class="fa-star"
            :class="index < Math.round(item.vote_average/2) ? 'fas' : 'far'"></i>
          </div>
          <p class="overview">{{item.overview}}</p>
         </div>
         
       </div>
        
     </template>
      
    </FlipFlopCard>
</template>

<script>

import FlipFlopCard from "vue-flip-flop-card";

export default {
  name: 'Card',
  components:{
    FlipFlopCard
  },
  props:{
    item: Object
  },
  data(){
    return{
      flags: ['it','en']
    }
  },
  computed:{
    
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars.scss';


.sc-card{
  .inner{
    padding: 5px; 
    height: 100%;
    .inner-back{
      height: 100%;
      background-color: lighten($bg-color, 20);
      padding: 5px;
    }
  }
  .overview{
    height: 48%;
    overflow-y: auto;
    margin-top: 5px;
    font-size: .8rem;
  }
  .cover{
    width: 100%;
  }
  
  .flag{
      width: 30px;
    }
  }


</style>