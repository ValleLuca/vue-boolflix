<template>
  <div @mouseover="active = true" @mouseleave="active = false">
    <div v-if="active">
        <h5>{{ info.titolo }}</h5>
        <h6>{{ info.titolo_originale }}</h6>
    </div>
    <div v-if="!active">
        <img class="img-fluid" :src="'https://image.tmdb.org/t/p/w500/' + info.immagine">
    </div>
    <div v-else>
        <img class="img-fluid" :src="getFlag( info.lingua )">
        <div class="d-flex justify-content-center">
            <div v-for="(dVoto, i) in arrBoxTot" :key="i">
                <div v-if="i <= 4">
                    <div v-if="dVoto.voto > i">
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
</template>

<script>
export default {
    name: "boxFilmSerie",
    props: {
    info: Object,
    arrBoxTot: Array

    },
    data(){
    return{
      active: false
        }
    },
    methods:{
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
    }
    }
}
</script>

<style>

</style>