<template>
  <div>
    <input v-model="search" type="text" placeholder="Certa il tuo film">
    <button @click="fetchMovies">Cerca</button>
    <!-- <select v-model="language" name="" id="">
      <option value=""></option>
      <option value="it">Italiano</option>
      <option value="fr">Francese</option>
      <option value="de">Tedesco</option>
      <option value="sp">Spagnolo</option>
      <option value="ab">Abkhazian</option>
    </select> -->
  
    <div class="main" v-for="(el,id) in filmList" :key="id">
      <p class="red">
        Titolo: {{el.title}}
      </p>
      <p class="green">
        Titolo Originale: {{el.original_title}}
      </p>
      <p class="magenta">
        Lingua Originale {{el.original_language}}   <img :src="`https://flagcdn.com/32x24/${el.original_language}.png`" alt="">
      </p>
      <p>
        Voto: {{el.vote_average}}
      </p>
    </div>

    <div class="main" v-for="(el,i) in seriesList" :key="el.name+i">
      <p class="magenta">
        Titolo Serie: {{el.name}}
      </p>
      <p class="green">
        Titolo Originale Serie: {{el.original_name}}
      </p>
      <p class="red">
        Lingua Originale Serie: {{el.original_language}} <img :src="imgLanguage" alt="">
      </p>
      <p>
        Voto Serie: {{el.vote_average}}
      </p>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      filmList: [],
      search: '',
      seriesList:[],
      language:'',
      imgLanguage:''
    }
  },

  methods: {
    fetchMovies() {
      if(this.search.trim()==='')
      return
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=c06469aaddab42d82abffd99307b058c&language=${this.language}&query=${this.search}`)
        .then((res) => {
          console.log(res.data.results);
          this.filmList = res.data.results;
        })
        .catch((err) => {
          console.log(err)
        })
        .finally(() => {
          console.log('finito nei film')
                 
        });

        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=c06469aaddab42d82abffd99307b058c&language=${this.language}&query=${this.search}`)
        .then((res) => {
          console.log(res.data.results, 'serie');
          this.seriesList = res.data.results;
        })
        .catch((err) => {
          console.log(err)
        })
        .finally(() => {
          console.log('finito nelle serie')
          
        })
        this.search=''
    },
    fetchFilm(){

    },
    fetchSeries(){}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.main {
  display: flex;
  gap: 10px;
  justify-content: center;
  align-items: center;


  .red {
    color: red;
  }

  .green {
    color: green;
  }

  .magenta {
    color: magenta;
  }
}
</style>
