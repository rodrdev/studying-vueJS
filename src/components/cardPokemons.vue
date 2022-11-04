<template>
<div class="card mt-5 mx-5" style="width: 18rem;">
  <img 
  v-bind:src="imagePokemon"
  class="imgLimitWidth card-img-top rounded-circle">
  <div class="text-center">
    <h1 class="card-title">{{pokemon.name.toUpperCase()}}</h1>
  </div>

</div>
</template>

<script>
export default {
    name: 'cardPokemons',
    props: {
      pokemon: Object,
    },
    data() {
      return {
        imagePokemon:''
      }
    },
    methods: {
 async getImagePokemon() {
    const req = await fetch(this.pokemon.url)
     const data = await req.json()
    
     this.imagePokemon = data.sprites.front_default.toString()
  }
},
mounted() {
    this.getImagePokemon()
  },
}
</script>

<style scoped>
  .imgLimitWidth {
    width: 150px;
    margin: auto;
  }
</style>