<template>
  <div class="hello">
    <h1>Lista de Pokemon</h1>
    <div class="container">
      <div class="card mb-6" style="max-width: 540px;">
        <div class="row g-0" v-for="pok in poke" :key="pok">
          <div class="col-md-4">
            <img :src="pok.images.small" class="bd-placeholder-img card-img-top" width="20%">
          </div>
          <div class="col-md-8">
            <div class="card-body">
              <h5 class="card-title">{{ pok.name }}</h5>
              <p>HP: {{ pok.hp }} </p>
              <p v-for="type in pok.types" :key="type">Tipo: {{ type }}</p>
              <p>Generación: {{ pok.set.series }}</p>
              <p>Rareza: {{ pok.rarity }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

const axios = require('axios');

export default {
  name: 'Pokemon',
  data() {
    return {
      poke: null
    }
  },
  mounted() {
    axios
    .get('https://api.pokemontcg.io/v2/cards')
    .then(response => (this.poke = response.data.data))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
