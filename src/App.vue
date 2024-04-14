<template>
  <buscador_cmp @conectaAPI = "conectaAPI"></buscador_cmp>
  <mostrador_cmp v-if="bResult" 
    :nombrePokemon="this.pokemon.name" 
    :idPokemon="this.pokemon.id" 
    :srcPokemon="this.pokemon.sprites.front_default" 
    :tipoPokemon="this.pokemon.types[0].type.name">
  </mostrador_cmp>
 
</template>

<script>
import buscador_cmp from "./components/buscador_cmp.vue";
import mostrador_cmp from "./components/mostrador_cmp.vue";

export default {
  name: 'App',
  components: {
    buscador_cmp,
    mostrador_cmp,
  },
  data(){
    return {
      pokemon: {
        name: '',
        id: '',
        sprites: {front_default: ''},
        types: [{type: {name: ''}}]
      },
      bResult:false,
      error:String,
    }
  },
  methods: {
    conectaAPI(message){
      fetch(`https://pokeapi.co/api/v2/pokemon/${message}`)
            .then(res => {
              res.json().then(json => {
                this.bResult = true
                this.pokemon = json
              console.log(this.pokemon)
            })
            .catch((err) => {
                this.bresult = false;
                this.error="El usuario no existe"
                console.error(err);
              });  
            })
    }
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  
}
</style>
