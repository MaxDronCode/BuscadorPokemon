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
    width: 250px;
    height: 250px;
}
.parrafo-tipo{
    padding-bottom: 40px;
    color: black;
    font-size: 20px;
}
</style>