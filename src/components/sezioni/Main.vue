<template>
  <section class="container">
    <div class="d-flex justify-content-center">
      <div class="p-4 d-flex flex-column align-items-center">
        <input type="text" class="text-center" placeholder="Cerca qui" v-model="inputRicercaUtente" @keyup="RicercaApiFilm"> 
        <!-- selezione lingua -->
        <div>
          <select name="lingua" @change="selezioneLingua">
              <option value="it-IT">Italiano</option>
              <option value="en-US">Inglese</option>
              <option value="es-ES">Spagnolo</option>
          </select>
        </div>
      </div>
    </div>
    <div class="row row-cols-5">
      <div class="col border d-flex flex-column justify-content-center text-center" v-for="(element, index) in arrayTotale" :key="index">
        <!-- caselle -->
          <h5>{{ element.titolo }}</h5>
          <h6>{{ element.titolo_originale }}</h6>
          <img class="img-fluid" :src="'https://image.tmdb.org/t/p/w500/' + element.immagine">
          <img class="img-fluid" :src="getFlag( element.lingua )">
          <p>{{ element.voto }}</p>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Main',
  data() {
    return {
      filmArray: [],
      serieArray: [],
      inputRicercaUtente: "",
      linguaSelezionata: "",
      cambiOggetto: "",
    }
  },
  created() {
    this.RicercaApiFilm();
    this.RicercaApiSerie();
  },
  computed: {
    arrayFilmAdattata(){
          const arrayObjMod = [];
          this.filmArray.forEach((elem) => {
            const objApp = {
              titolo: elem.title,
              titolo_originale: elem.original_title,
              lingua: elem.original_language,
              voto: elem.vote_average,
              immagine: elem.poster_path,
            };
            arrayObjMod.push(objApp);
          });
          return arrayObjMod;
        },
    arraySerieAdattata(){
      const arrayObjMod = [];
      this.serieArray.forEach((elem) => {
        const objApp = {
          titolo: elem.name,
          titolo_originale: elem.original_name,
          lingua: elem.original_language,
          voto: elem.vote_average,
          immagine: elem.poster_path,
        };
        arrayObjMod.push(objApp);
      });
      return arrayObjMod;
    },
    arrayTotale() {
      return [...this.arrayFilmAdattata, ...this.arraySerieAdattata];
    }
     
  },
  methods: {
    getFlag( language )
    {
      if(language == "en"){
        language = "gb"
      }
      if (language == "ja") {
        language = "jp"
      }
      return 'https://countryflagsapi.com/png/' + language
    },
    RicercaApiFilm: function() {
      axios.get("https://api.themoviedb.org/3/search/movie", 
      {
        params: {
          api_key: '87fc6a59479bfaf6ae9b13c70ef1655e',
          language: this.linguaSelezionata,
          query: this.inputRicercaUtente
        }
      })
      .then( (dato) => {
        this.filmArray = dato.data.results;
        this.RicercaApiSerie();
      })
      .catch(function (error) {
        console.log(error);
      })
      .then(function () {
        // always executed
      });
    },
    RicercaApiSerie: function() {
      axios.get("https://api.themoviedb.org/3/search/tv", 
      {
        params: {
          api_key: '87fc6a59479bfaf6ae9b13c70ef1655e',
          language: this.linguaSelezionata,
          query: this.inputRicercaUtente
        }
      })
      .then( (dato) => {
        this.serieArray = dato.data.results;
      })
      .catch(function (error) {
        console.log(error);
      })
      .then(function () {
        // always executed
      });
    },
    selezioneLingua(e) 
    {
      this.linguaSelezionata = e.target.value;
      console.log(this.linguaSelezionata);
      this.RicercaApiFilm();
    },
    modificaVoto () {
      this.arrayFilmAdattata.forEach((elem) => {
      console.log(elem[0].voto);
      });
    }
  }
}
//Math.ceil ciò che ci serve
</script>

<style scoped lang="scss">

</style>