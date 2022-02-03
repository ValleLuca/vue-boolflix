<template>
  <section class="container">
    <div class="d-flex justify-content-center">
      <div class="p-4">
        <input type="text" placeholder="Cerca qui" v-model="inputRicercaUtente" @keyup="RicercaApi">
        <div>
          <select name="lingua" @change="selezioneLingua">
              <option value="">Scegli il genere</option>
              <option value="it-IT"><img src="../img/it.png"></option>
              <option value="en-US">Inglese</option>
              <option value="es-ES">Spagnolo</option>
              <option value="ie-IE">Altre</option>
          </select>
        </div>
      </div>
    </div>
    <div class="row row-cols-5">
      <div class="col border text-center" v-for="(element, index) in filmArray" :key="index">
        <!-- caselle -->
          <h5>{{ element.title }}</h5>
          <h6>{{ element.original_title }}</h6>
          <p>{{ element.original_language }}</p>
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
    selezioneLingua(e) {
      this.linguaSelezionata = e.target.value;
      console.log(this.linguaSelezionata);
    }
    
  }
}

</script>

<style scoped lang="scss">

</style>