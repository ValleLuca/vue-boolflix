<template>
  <section class="container">
    <div class="d-flex justify-content-center">
      <div class="p-4">
        <input type="text" placeholder="Cerca qui" v-model="inputRicercaUtente" @keyup="ricerca">
        <button>Ricerca</button>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <!-- caselle -->
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
    }
  },
  created() {
    this.RicercaApi();
  },
  methods: {
    RicercaApi: function() {
      axios.get("https://api.themoviedb.org/3/movie", {
      params: {
        api_key: '87fc6a59479bfaf6ae9b13c70ef1655e',
        query: 'fast'
      }
      })
      .then( (dato) => {
        this.filmArray = dato.api_key.query;
        console.log(dato.data);

      })
      .catch(function (error) {
        console.log(error);
      })
      .then(function () {
        // always executed
      });
    }
    
  }
}

</script>

<style scoped lang="scss">

</style>