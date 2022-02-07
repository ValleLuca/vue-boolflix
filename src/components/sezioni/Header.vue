<template>
  <div>
    <div class="d-flex bg-black align-items-center flex-column">
      <div class="p-4">
        <h2 class="text-danger">BOOLFLIX</h2>  
      </div>

      <div class="d-flex justify-content-center">
        <div class="p-4 d-flex flex-column align-items-center">
          <input type="text" class="text-center" placeholder="Cerca qui" v-model="inputRicercaUtente" @keyup="$emit('ricerca', inputRicercaUtente)"> 
          <!-- selezione lingua -->
          <div>
            <select name="lingua" v-model="selectlingua" @change="$emit('selezione', selectlingua)">
                <option value="it-IT">Italiano</option>
                <option value="en-US">Inglese</option>
                <option value="es-ES">Spagnolo</option>
            </select>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      inputRicercaUtente: "",
      selectlingua: ""
    };
  }
}
</script>

<style scoped lang="scss">

</style>
