<template>
  <buscador @conectaAPI = "conectaAPI"></buscador>
</template>

<script>
import buscador from "./components/buscador-cmp.vue";
export default {
  name: 'App',
  components: {
    buscador
  },
  methods: {
    conectaAPI(message){
      fetch(`https://pokeapi.co/api/v2/pokemon/${message}`)
            .then(res => {
              res.json().then(json => {
                this.bresult = true
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
