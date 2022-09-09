<template>
  <div>
    <input v-model="search" type="text" placeholder="Certa il tuo film"> 
    <button @click="fetchMovies" >We</button>
    <div v-for="(el,id) in filmList" :key="id">
      {{el.original_title}}</div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      filmList: [],
      search:''
    }
  },

  methods: {
    fetchMovies() {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=c06469aaddab42d82abffd99307b058c&query=${this.search}`)
        .then((res) => {
          console.log(res.data.results);
          this.filmList = res.data.results;
        })
        .catch((err) => {
          console.log(err)
        })
        .finally(() => {
          console.log('finito')
          this.search=''
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
