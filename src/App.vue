<template>
  <div id="app">
    <Header @ricerca="ricercaCompletata" @selezione="selezioneLingua"/>
    <Main :ArTot="arrayTotale"/>
  </div>
</template>

<script>
import Header from './components/sezioni/Header.vue'
import Main from './components/sezioni/Main.vue'
import axios from 'axios'



export default {
  name: 'App',
  components: {
    Header,
    Main
},
  data() {
  return {
    filmArray: [],
    serieArray: [],
    inputRicercaUtente: "",
    linguaSelezionata: "",
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

    ricercaCompletata(dato) {
      this.inputRicercaUtente = dato;
      this.RicercaApiFilm();
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
        this.modificaVotoFilm();
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
        this.modificaVotoSerie();
      })
      .catch(function (error) {
        console.log(error);
      })
      .then(function () {
        // always executed
      });
    },
    selezioneLingua(lingua) 
    {
      this.linguaSelezionata = lingua;
      console.log(this.linguaSelezionata);
      this.RicercaApiFilm();
    },
    modificaVotoFilm () {
      this.arrayFilmAdattata.forEach((elem, i) => {
      let divisione = (elem.voto / 2);
      let stelle = (Math.ceil(divisione));
      this.arrayFilmAdattata[i].voto = stelle;
      });
    },
    modificaVotoSerie () {
      this.arraySerieAdattata.forEach((elem, i) => {
      let divisione = (elem.voto / 2);
      let stelle = (Math.ceil(divisione));
      this.arraySerieAdattata[i].voto = stelle;
      });
    }
  }
}
</script>

<style lang="scss">
@import "./assets/style/Global.scss";

</style>
