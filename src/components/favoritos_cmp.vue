<template>
    <div class="container-pokemon">
        <div class="datos-pokemon">
            <p class="id-pokemon">{{ idPokemon }}</p>
            <p class="nombre-pokemon">{{ nombrePokemon }}</p>
        </div>
        <img :src="srcPokemon" alt="" class="img-pokemon">
    </div>
</template>

<script>
    export default{
        name: "favoritos_cmp",

        props:{
            idPokemon:Number,
            nombrePokemon:String,
            srcPokemon:String,
        }
    }
</script>

<style scoped>
.container-pokemon{
    box-sizing: content-box;
    width: 150px;
    height: 150px;
    margin-top: 80px;
    color:whitesmoke;
    box-shadow: 0 0 2px 2px #303646;
}
.datos-pokemon{
    display: flex;
    justify-content: space-around;
}
.img-pokemon{
    padding: 0;
}
</style>