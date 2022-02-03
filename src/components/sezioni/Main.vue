<template>
  <section class="container">
    <div class="d-flex justify-content-center">
      <div class="p-4">
        <input type="text" placeholder="Cerca qui" v-model="inputRicercaUtente" @keyup="RicercaApi">  <!--  -->
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
      inputRicercaUtente: ""
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
          query: this.inputRicercaUtente
        }
      })
      .then( (dato) => {
        this.filmArray = dato.data.results;
        console.log(this.filmArray);

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