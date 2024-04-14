<template>
    <div id="container-pokemon" class="container-pokemon">
        <p id="nombrePokemon" class="nombrePokemon">{{ nombreMayuscula }}</p>
        <div id="container2-pokemon" class="container2-pokemon">
            <div id="container-id" class="container-id">
                <p id="parrafo-id" class="parrafo-id">ID</p>
                <p id="numero-ud" class="numero-id">{{ idPokemon }}</p>
            </div>
            <img :src="srcPokemon" alt="Imagen del Pokemon">
            <p id="parrafo-tipo" class="parrafo-tipo">{{ tipoMayuscula }}</p>
            <button class="btnFavoritos" @click="toggleFavorito">{{ favoriteButtonText }}</button>
        </div> 
    </div>
</template>

<script>
export default {
  name: 'mostrador_cmp',
  
  props:{
    nombrePokemon:String,
    idPokemon:Number,
    srcPokemon:String,
    tipoPokemon:String,
    favoriteButtonText:String,
  },
  methods: {
    toggleFavorito(){
        this.$emit("toggleFavorito")
    }
  },

  computed:{
    nombreMayuscula(){
        return this.nombrePokemon.charAt(0).toUpperCase() + this.nombrePokemon.slice(1);
        
    },
    tipoMayuscula(){
        return this.tipoPokemon.charAt(0).toUpperCase() + this.tipoPokemon.slice(1);
    }
  }
  
}
</script>

<style scoped>
.container-pokemon{
    box-sizing: content-box;
    /* border: 1px solid #828DA9; */
    box-shadow: 0 0 2px 2px #303646;
    border-radius: 4px;
    width: 420px;
    margin: 30px auto;
}
.nombrePokemon{
    width: 300px;
    border-bottom: 1px solid whitesmoke;
    font-size: 30px;
    margin: auto;
}
.container-id{
    display: flex;
    justify-content: space-around;
}
img{
    box-sizing: content-box;
    width: 180px;
    height: 180px;
}
.parrafo-tipo{
    /* padding-bottom: 40px; */
    color: black;
    font-size: 20px;
}
.btnFavoritos {
  min-width: 130px;
  height: 40px;
  color: #fff;
  margin-bottom: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  display: inline-block;
  outline: none;
  border: 1px solid #000;
  border-radius: 2px;
  color: #000;
  background: transparent;
  z-index: 0;
  
}
.btnFavoritos:hover:after {
  top: 0;
  left: 0;


}
.btnFavoritos:after {
  content: "";
  width: 100%;
  z-index: -1;
  position: absolute;
  height: 100%;
  top: 5px;
  left: 5px;
  transition: 0.2s;
  background-color: #ffe566;
  border-radius: 2px;

}
</style>