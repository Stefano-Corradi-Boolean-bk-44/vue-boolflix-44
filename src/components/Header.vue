<template>
  <header class="d-flex justify-content-between p-3">

    <div class="logo">
      <img src="../assets/img/logo-boolflix.png" alt="">
    </div>

    <div class="d-flex">
      <input
      class="form-control"
      v-model="textToSearch"
      @keyup.enter="$emit('sendSearch',textToSearch, typeToSerach)"
     type="text" placeholder="Cerca un film">

     <select
      v-model="typeToSerach"
      @change="$emit('sendSearch',textToSearch, typeToSerach)"
      class="form-select ms-3" >
        <option value="">All</option>
        <option value="movie">Film</option>
        <option value="tv">Serie Tv</option>
      </select>

    </div>
    

  </header>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return{
      textToSearch:'',
      typeToSerach:''
    }
  }
}
</script>

<style lang="scss" scoped>

@import '../assets/style/vars.scss';


header{
  height: 70px;
  background-image: linear-gradient(black, $bg-color);
  .logo{
    img{
      width: 150px;
    }
  }
  input{
    min-width: 400px;
  }
}
</style>