<template>
  <section class="container">
    <div class="row row-cols-5">
      <div class="col border d-flex flex-column justify-content-center text-center" v-for="(element, index) in ArTot" :key="index">
        <!-- caselle -->
        <BoxFilmSerie :info="element" :arrBoxTot="ArTot"/>
      </div>
    </div>
  </section>
</template>

<script>
import BoxFilmSerie from './boxFilmSerie.vue'

export default {
  name: 'Main',
  components: {
    BoxFilmSerie,
  },
  props: {
    ArTot: Array
  }
}
</script>

<style scoped lang="scss">


</style>