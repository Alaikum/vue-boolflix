<template>
  <div>
    <input v-model="search" type="text" placeholder="Cerca il tuo film" @keyup.enter="fetchMovies">
    <button @click="fetchMovies">Cerca</button>


    <!-- <select v-model="language" name="" id="">
      <option value=""></option>
      <option value="it">Italiano</option>
      <option value="fr">Francese</option>
      <option value="de">Tedesco</option>
      <option value="sp">Spagnolo</option>
      <option value="ab">Abkhazian</option>
    </select> -->

    <!-- <CardMovie v-for="(el,id) in filmList" :key="id" :filmList='filmList'/> -->
 <div class="main" v-for="(el,id) in filmList" :key="id"> 
      <p class="red">
        Titolo: {{el.title}}
      </p>
      <p class="green">
        Titolo Originale: {{el.original_title}}
      </p>
      <p class="magenta">
        Lingua Originale {{el.original_language}}
      </p>
      <figure>
        <img :src="`https://flagcdn.com/32x24/${el.original_language}.png`" alt="">
      </figure>

      <p>
        Voto:
        <span v-for="n in voteStar(el)" :key="n">
          <font-awesome-icon icon="fa-solid fa-star" />
        </span>
        <span v-for="(star) in (5 -voteStar(el))" :key="star+el.original_title">
          <font-awesome-icon icon="fa-regular fa-star" />
        </span>

      </p>
      <figure>
        <img :src="posterPhoto(el)" alt="Poster Not Found">
      </figure>
    </div>

    <div class="main" v-for="(el,i) in seriesList" :key="el.name+i">
      <p class="magenta">
        Titolo Serie: {{el.name}}
      </p>
      <p class="green">
        Titolo Originale Serie: {{el.original_name}}
      </p>
      <p class="red">
        Lingua Originale Serie: {{el.original_language}}
      </p>
      <figure>
        <img :src="`https://flagcdn.com/32x24/${el.original_language}.png`" alt="">

      </figure>
      <p>
        Voto Serie:
        <span v-for="n in voteStar(el)" :key="n">
          <font-awesome-icon icon="fa-solid fa-star" />
        </span>
        <span v-for="(star) in (5 -voteStar(el))" :key="star+el.original_name">
          <font-awesome-icon icon="fa-regular fa-star" />
        </span>
      </p>
      <figure>
        <img :src="posterPhoto(el)" alt="Poster Not Found">
      </figure>
    </div> -->
  </div>
</template>

<script>
import axios from 'axios';
// import CardMovie from './CardMovie.vue';

export default {
    data() {
        return {
            filmList: [],
            search: "",
            seriesList: [],
            imgFlag: "",
            BASE_URI: "https://api.themoviedb.org/3",
            api_key: "c06469aaddab42d82abffd99307b058c",
            language: "it-IT"
        };
    },
    computed: {
        votazione() {
            return null;
        }
    },
    methods: {
        fetchMovies() {
            if (this.search.trim() === "")
                return;
            this.fetchFilm();
            this.fetchSeries();
        },
        fetchFilm() {
            // axios.get(`${this.BASE_URI}/search/movie?api_key=c06469aaddab42d82abffd99307b058c&${this.language}&query=${this.search}`)
            axios.get(`${this.BASE_URI}/search/movie`, {
                params: {
                    api_key: this.api_key,
                    language: this.language,
                    query: this.search
                }
            })
                .then((res) => {
                // console.log(res.data.results);
                this.filmList = res.data.results;
                this.translateFlags(this.filmList);
            })
                .catch((err) => {
                console.log(err);
            })
                .finally(() => {
                console.log("finito nei film");
            });
        },
        fetchSeries() {
            // axios.get(`https://api.themoviedb.org/3/search/tv?api_key=c06469aaddab42d82abffd99307b058c&language=${this.language}&query=${this.search}`)
            axios.get(`${this.BASE_URI}/search/tv`, {
                params: {
                    api_key: this.api_key,
                    language: this.language,
                    query: this.search
                }
            })
                .then((res) => {
                // console.log(res.data.results, 'serie');
                this.seriesList = res.data.results;
                this.translateFlags(this.seriesList);
            })
                .catch((err) => {
                console.log(err);
            })
                .finally(() => {
                console.log("finito nelle serie");
            });
            this.search = "";
        },
        // getFlags(el){
        //   axios.get(`https://flagcdn.com/32x24/${el.original_language}.png`)
        //     .then((res) => {
        //       console.log(el,res.data);
        //       // this.seriesList = res.data.results;
        //       // this.translateFlags(this.seriesList)
        //     })
        //     .catch((err) => {
        //       console.log(err)
        //     })
        //     .finally(() => {
        //       console.log('fine flags')
        //     })
        // },
        posterPhoto(el) {
            if (el.poster_path === null) {
                return;
            }
            return `https://image.tmdb.org/t/p/w92/${el.poster_path}`;
        },
        voteStar(el) {
            // console.log(el.vote_average)
            let votoStelle = Math.ceil(el.vote_average / 2);
            console.log(votoStelle, "stelle");
            return votoStelle;
        },
        translateFlags(el) {
            console.log(el);
            el.forEach(el => {
                if (el.original_language == "en") {
                    el.original_language = "gb";
                }
                if (el.original_language == "hi") {
                    el.original_language = "in";
                }
                if (el.original_language == "ja") {
                    el.original_language = "jp";
                }
                if (el.original_language == "fa") {
                    el.original_language = "ir";
                }
                if (el.original_language == "ko") {
                    el.original_language = "kr";
                }
                if (el.original_language == "cs") {
                    el.original_language = "cz";
                }
                if (el.original_language == "zh") {
                    el.original_language = "cn";
                }
                if (el.original_language == "uk") {
                    el.original_language = "ua";
                }
                if (el.original_language == "da") {
                    el.original_language = "dk";
                }
            });
        }
    },
    // components: { CardMovie }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.main {
  display: flex;
  gap: 10px;
  justify-content: center;
  align-items: center;

  figure {
    margin: 0;
  }

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
