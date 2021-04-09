<template>
  <div class="hello">
    <h1>Cartas</h1>
    <br>
    <div class="row row-cols-1 row-cols-md-3 g-4">
      <div class="col" v-for="(pok,index) in pokemons" :key="index">
        <div class="card">
          <br>
          <img :src="pok.images.small" alt="" style="width: 50%" class="mx-auto d-block">
          <div class="card-body">
            <h5 class="card-tile">{{ pok.name }}</h5>
            <p class="card-text"><b>HP:</b> {{ pok.hp }}</p>
            <p class="card-text" v-for="type in pok.types" :key="type"><b>Tipo:</b> 
              {{ type }}
            </p>
            <p class="card-text"><b>Generación:</b> {{ pok.set.series }}</p>
            <p class="card-text"><b>Rareza:</b> {{ pok.rarity }}</p>
            <p class="card-text" v-for="attack in pok.attacks" :key="attack"><b>Ataques: </b>
              {{ attack.name }}
            </p>
            <p class="card-text" v-for="debil in pok.weaknesses" :key="debil"><b>Debilidad: </b>
              {{ debil.type }} {{ debil.value }}
            </p>
            <!-- Button trigger modal -->
              <button type="button" class="btn btn-primary" data-bs-toggle="modal" :data-bs-target="'#modal' + index" @click="handlePokemon(pok.name.toLowerCase())">
                Ver detalles Pokemon
              </button>

              <!-- Modal -->
              <div class="modal fade" :id="'modal' + index" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">{{ pok.name }}</h5>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <img :src="pokemon.sprites.front_default" alt="" style="width: 50%" class="mx-auto d-block">
                      <span>
                        <b>Experiencia base:</b> {{ pokemon.base_experience }} XP 
                      </span><br>
                      <span>
                        <b>Altura: </b> {{ pokemon.height }} m
                      </span><br>
                      <span>
                        <b>Peso: </b> {{ pokemon.weight }} kg
                      </span><br>
                      <span>
                        <b>Tipo: </b> 
                        <span v-for="(value, index) in pokemon.types" :key="'value'+index">
                          {{ value.type.name }}
                        </span>
                      </span><br>
                      <span>
                        <b>Habilidades:</b>
                        <span v-for="(value, index) in pokemon.abilities" :key="'value'+index">
                          {{ value.ability.name }}
                        </span>
                      </span>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                      <button type="button" class="btn btn-primary">Save changes</button>
                    </div>
                  </div>
                </div>
              </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

const axios = require('axios');

// function hola() {
//   alert('Hola simplemente');
// }

export default {
  name: 'Pokemon',
  data() {
    return {
      pokemons: [],
      name: '',
      pokemon: {
        sprites: {
          front_default: ''
        }
      }
    }
  },
  created() {
    this.handleCards();
  },
  mounted() {
    // hola();
    // axios
    // .get('https://api.pokemontcg.io/v2/cards')
    // .then(response => (this.poke = response.data.data))
    // this.handleCards();
  },
  methods: {
    handleCards() {
      this.sendApi('https://api.pokemontcg.io/v2/cards')
      .then(response => (this.pokemons = response.data.data));
    },
    handlePokemon(name = 'pikachu') {
      this.sendApi(`https://pokeapi.co/api/v2/pokemon/${name}`)
      .then(response => (this.pokemon = response.data));
    },
    sendApi(url) {
      return axios
      .get(url)
      .then(response => {return response;});
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
