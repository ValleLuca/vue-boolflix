<template>
  <section class="container">
    <div class="d-flex justify-content-center">
      <div class="p-4 d-flex flex-column align-items-center">
        <input type="text" class="text-center" placeholder="Cerca qui" v-model="inputRicercaUtente" @keyup="RicercaApi">
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
      <div class="col border d-flex flex-column justify-content-center text-center" v-for="(element, index) in filmArray" :key="index">
        <!-- caselle -->
          <h5>{{ element.title }}</h5>
          <h6>{{ element.original_title }}</h6>
          <img class="img-fluid" :src="getFlag( element.original_language )">
          <p>{{ element.vote_average }}</p>
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
      inputRicercaUtente: "",
      linguaSelezionata: ""
    }
  },
  created() {
    this.RicercaApi();
  },
  methods: {
    getFlag( language )
    {
      if(language == "en"){
        language = "gb"
      }
      return 'https://countryflagsapi.com/png/' + language
    },
    RicercaApi: function() {
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
      this.RicercaApi()
    }
    
  }
}

</script>

<style scoped lang="scss">

</style>