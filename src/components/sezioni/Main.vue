<template>
  <section class="container">
    <div class="row row-cols-5">
      <div class="col border d-flex flex-column justify-content-center text-center" v-for="(element, index) in ArTot" :key="index">
        <!-- caselle -->
        <div @mouseover="active = true" @mouseleave="active = false">
          <div v-if="active">
            <h5>{{ element.titolo }}</h5>
            <h6>{{ element.titolo_originale }}</h6>
          </div>
          <div v-if="active == false">
            <img class="img-fluid" v-show!="ho" :src="'https://image.tmdb.org/t/p/w500/' + element.immagine">
          </div>
          <div v-if="active">
            <img class="img-fluid" :src="getFlag( element.lingua )">
            <div class="d-flex justify-content-center">
              <div v-for="(dVoto, i) in ArTot" :key="i">
                <div v-if="i <= 4">
                  <div v-if="element.voto > i">
                    <i class="fas fa-star"></i>
                  </div>
                  <div v-else>
                    <i class="far fa-star"></i>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: 'Main',
  props: {
    ArTot: Array
  },
  data(){
    return{
      active: false
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
      if(language == "hi")
      {
        language = "in"
      }
      if(language == "el")
      {
        language = "gr"
      }
      if(language == "da")
      {
        language = "dk"
      }
      if(language == "ko")
      {
        language = "kr"
      }
      if(language == "cs")
      {
        language = "cz"
      }
      return 'https://countryflagsapi.com/png/' + language
    },
  }
}
//Math.ceil ciò che ci serve 
</script>

<style scoped lang="scss">


</style>