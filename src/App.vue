<template>
  <div id="app">

    <Navbar />

    <div class="container">
      <div class="columns">
      <div class="column is-half is-offset-one-quarter desce">
        <img id="pokebola" src="./assets/pokemon.svg" alt="pokebola">
        <p class="is-size-3">Pokedex</p>
        <hr>
        <input type="text" placeholder="Buscar pokemon pelo nome" class="input" v-model="busca" @keyup.enter="buscar">
        <!-- <button class="button is-fullwidth is-danger" id="buscaBtn" @click="buscar">Buscar</button> -->
        
          <div class="field">
            <div class="control">
              <div class="select  is-danger">
                <select>
                  <option>type</option>
                  <option v-for="type in types" :key="type.name">{{ type.name }}</option>
                </select>
              </div>
            </div>
          </div>

      </div>
      </div>

      <div id="poke-container">
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
        </div>
      </div>

      <Pagination />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
// import _ from 'lodash';

import Navbar from './components/Navbar.vue';
import Pokemon from './components/Pokemon.vue';
import Pagination from './components/Pagination.vue';

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      types: [],
      busca: '',
      type: 'type'
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    }),
    axios.get("https://pokeapi.co/api/v2/type").then(res => {
      this.types = res.data.results;
      console.log(this.types);
    })
  },
  components: {
    Pokemon,
    Pagination,
    Navbar
  },
  methods: {
    buscar: function() {

      this.filteredPokemons = this.pokemons;

      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  computed: {
    // alphabeticOrder(){
    //   return _.orderBy(this.pokemons, ['name'], ['asc']);
    // }

    // resultadoBusca: function() {
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    //   }
    // }
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osz-font-smoothing: grayscale;
    text-align: center;
    color: #223355;
  }

  .desce {
    margin-top: 70px;
  }

  button {
    font-weight: bold;
  }

  #buscaBtn {
    margin-top: 2%;
  }

  #pokebola {
    max-width: 50px;
  }

  #poke-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 10px;
  }
</style>
