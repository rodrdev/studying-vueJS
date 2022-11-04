<template>
<div class="container">
  <div class="text-center">
    <input v-model="search" placeholder="Procure seu pokemon" style="width: 300px" type="text" class="mt-3  rounded-sm ">
  </div>
  <div class="row">
 <div v-for="(pokemon, index) in itemFiltered" class="col-4">
  <CardPokemons   :pokemon="pokemon"  />
 </div>
</div>
  </div>
</template>

<script>
import CardPokemons from './components/cardPokemons.vue'

export default {
  name: "App",
  components: {
    CardPokemons
    },
    data(){
      return {
        pokemons: [],
        search: ""
        
      }
    },
    filters: {
      toUpperCase(str) {
        return str.toUpperCase()
      }
    },
methods: {
   async getPokemons() {
     const req = await fetch("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0")
     const data = await req.json()
     console.log(data.results)
     this.pokemons = data.results
  },
 },
 mounted() {
    this.getPokemons()
  },
  computed: {
    itemFiltered() {
      let pokemonsFiltered = []

    pokemonsFiltered = this.pokemons.filter((pokemon) => pokemon.name.toLowerCase().indexOf(this.search.toLowerCase()) > - 1)
      return pokemonsFiltered
    }
  }
}

</script>