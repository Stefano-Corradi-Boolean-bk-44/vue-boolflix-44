<template>
  <main>

    <h1 class="container">
      {{titleSection}}
    </h1>

    <div class="container d-flex flex-wrap">
      <Card
      v-for="item in listResult"
      :key="item.id"
      :item='item'
     /> 
    </div>
    


  </main>
</template>

<script>

import Card from './Card'

export default {
  name: 'Main',
  components :{
    Card
  },
  props:{
    listResult: Array,
    titleSection: String
  }
}
</script>

<style>

</style>