<template>
  <buscador_cmp @conectaAPI="conectaAPI"></buscador_cmp>

  <mostrador_cmp v-if="bResult" 
    :nombrePokemon="this.pokemon.name" 
    :idPokemon="this.pokemon.id"
    :srcPokemon="this.pokemon.sprites.front_default" 
    :tipoPokemon="this.pokemon.types[0].type.name"
    :favoriteButtonText="favoriteButtonText"
    @toggleFavorito="toggleFavorito">
  </mostrador_cmp>
  <div class="favoritos-cmp-div">

    <favoritos_cmp v-for="favorito in arrayFavoritos" :key="favorito.id"
    :idPokemon="favorito.id"
    :nombrePokemon="favorito.name" 
    :srcPokemon="favorito.sprites.front_default" 
    >
    </favoritos_cmp>

  </div>

</template>

<script>
import buscador_cmp from "./components/buscador_cmp.vue";
import mostrador_cmp from "./components/mostrador_cmp.vue";
import favoritos_cmp from "./components/favoritos_cmp.vue";

export default {
  name: 'App',
  components: {
    buscador_cmp,
    mostrador_cmp,
    favoritos_cmp,
  },
  data() {
    return {
      pokemon: {
        name: '',
        id: '',
        sprites: { front_default: '' },
        types: [{ type: { name: '' } }]
      },
      bResult: false,
      error: String,
      favoritos: new Map(),
    }
  },

  computed: {
    favoriteButtonText() {
      return this.estaEnFavoritos ? 'Eliminar Favorito' : 'Añadir a Favoritos';
    },
    arrayFavoritos() {
      return Array.from(this.favoritos.values());
    },
    estaEnFavoritos() {
      return this.favoritos.has(this.pokemon.id);
    },
    existenFavoritos() {
      return this.favoritos.size > 0;
    }
  },

  methods: {
    conectaAPI(message) {
      fetch(`https://pokeapi.co/api/v2/pokemon/${message}`)
        .then(res => {
          res.json().then(json => {
            this.bResult = true
            this.pokemon = json
            console.log(this.pokemon)
          })
            .catch((err) => {
              this.bresult = false;
              this.error = "El usuario no existe"
              console.error(err);
            });
        })
    },
    actualizarLocalStorage(){
      localStorage.setItem("pokemonApi", JSON.stringify(this.arrayFavoritos))
    },

    toggleFavorito() {      
      if (this.favoritos.has(this.pokemon.id)) {
        this.favoritos.delete(this.pokemon.id);
        console.log("Favorito eliminado")
        console.log(this.favoritos)
      } else {
        this.favoritos.set(this.pokemon.id, this.pokemon);
        console.log("Favorito añadido")
        console.log(this.favoritos)
      }
      this.actualizarLocalStorage();
    },
    sacarDelLocalStorage(){
      const favoritosJSON = localStorage.getItem("pokemonApi")
      if (favoritosJSON){
        this.favoritos = new Map(JSON.parse(favoritosJSON).map(pokemon => [pokemon.id, pokemon]))
      }
    }
    
  },
  mounted(){
    this.sacarDelLocalStorage()
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
.favoritos-cmp-div{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
